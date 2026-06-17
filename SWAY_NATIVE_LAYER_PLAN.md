# Sway Native Layer — Product + Engineering Execution Plan
**Status:** Summer 2026 build. Target: Fall 2026 redeployment at Gully's + Endicott campus graph.  
**Stack:** React + Vite + Tailwind + shadcn/ui + Supabase + React Router + TanStack Query + Framer Motion  
**Agent read-order:** Architecture → Schema → Completion Engine → Roadmap → Flows → Tickets → Prompts

---

## What's being rebuilt and why

The current system rewards a tap instantly (`points_earned` on `check_ins` insert). That's wrong. The new model is:

**Tap = intent. Completion = credit.**

Nothing is awarded on scan. Credit is issued only after a presence session closes as "completed." This document tells coding agents exactly how to get there.

---

## 1. Product Architecture — Module Map

### 1.1 User Identity
**What it does:** Single auth identity (Supabase Auth) tied to a portable profile. Carries display name, school, avatar, class year, Sway Card, status level, global participation stats.  
**Key tables:** `student_profiles`, `user_global_stats`, `sway_cards`  
**NOT in scope:** social graph, followers, public profiles

### 1.2 Place Nodes
**What it does:** A physical location that can host sessions. Gully's is a place. The campus gym is a place. Foundry room is a place.  
**Key tables:** `places` (replaces/extends `venues`)  
**Fields:** name, type (bar/gym/event_space/academic/outdoor), address, campus, node_code (QR/NFC entry code), active, venue_status  
**NOT in scope:** POS integration, menu, ordering

### 1.3 Community Nodes
**What it does:** A group that exists independent of a single place. Entrepreneurship Club, soccer team, senior class. Communities host events. Members can be tracked across places.  
**Key tables:** `communities`, `community_members`  
**Fields:** name, type (club/team/program/class/campus), campus, admin_user_id

### 1.4 Event Nodes
**What it does:** A time-bounded session hosted by a place or community. Trivia night, pitch night, sports game, gym class. Events define the participation window for session completion.  
**Key tables:** `events`  
**Fields:** title, description, place_id, community_id (nullable), start_at, end_at, completion_window_minutes, status (draft/active/closed)

### 1.5 Check-ins
**What it does:** Records the moment a user scans into a place or event. This is the INPUT, not the output. Nothing is credited here.  
**Key tables:** `check_ins`  
**Fields:** user_id, place_id, event_id (nullable), scanned_at, source (qr/nfc/wallet/staff), client_ip, device_fingerprint  
**Key rule:** NO points, NO status update on insert. Check-in only opens a session.

### 1.6 Presence Sessions
**What it does:** The core primitive. A session is opened when a check-in occurs and closes as completed/incomplete/suspicious based on validation logic. Credit is issued ONLY on a completed session.  
**Key tables:** `presence_sessions`, `session_validation_events`  
**Fields:** user_id, place_id, event_id, opened_at, closed_at, status (open/completed/incomplete/suspicious), completion_method, participation_credits_issued  
**Key rule:** Session status drives everything. Status ≠ completed → no credit.

### 1.7 Sway Cards
**What it does:** A visual identity credential. Displays user name, status tier, total completed sessions, active nodes, class year. Feels like a membership card, not a punch card.  
**Key tables:** `sway_cards`  
**Fields:** user_id, card_number (formatted display ID), tier, total_sessions, active_node_count, issued_at, last_updated_at  
**UI:** Dark card, user photo, tier badge, session count, tap-to-share. No points displayed.

### 1.8 Status / Progression
**What it does:** Behavioral identity ledger. NOT points → money. Tiers reflect how much someone has actually shown up. Tier names should be identity words, not loyalty-app words.  
**Tier model:**
- **Newcomer** — 0 completed sessions
- **Familiar** — 3+ completed sessions at any node
- **Regular** — 7+ completed sessions, 2+ distinct nodes
- **Known** — 15+ completed sessions, 3+ distinct nodes
- **Embedded** — 30+ completed sessions, 4+ distinct nodes  
**Key tables:** `user_global_stats` (computed), `user_node_stats` (per place/community)  
**Key rule:** Tier is calculated from `presence_sessions WHERE status = 'completed'`. Never from check-in count.

### 1.9 Timeline / Memory Layer
**What it does:** A reverse-chronological personal record of completed sessions. "You were at Gully's trivia night. You checked into the gym 4 times this week. You were at pitch night."  
**Key tables:** `presence_sessions` (the timeline IS the sessions), `recaps`  
**UI:** Card-based feed. Each entry shows place, event (if any), time, session type. No clutter.

### 1.10 Recaps
**What it does:** Periodic summaries generated for users. Weekly: where you showed up. Monthly: your most active node. Semester: full participation story.  
**Key tables:** `recaps`  
**Fields:** user_id, recap_type (weekly/monthly/semester), period_start, period_end, data_json (structured summary), generated_at

### 1.11 Circles / Social Graph
**What it does:** Small private groups. Friend group, study team, intramural team. Circles let users see who they overlap with across nodes.  
**Key tables:** `circles`, `circle_members`  
**Fields (circles):** name, created_by, invite_code, is_private  
**Fields (circle_members):** circle_id, user_id, joined_at, role  
**Phase 3+ only.** Do not build in Phase 0–1.

### 1.12 Operator Dashboard
**What it does:** Venue/community operator sees participation signal. Who came back. What event drove return. Who are the emerging regulars. Read-only analytics. No staff workflow changes.  
**Key tables:** Reads from `presence_sessions`, `user_node_stats`, `events`  
**Users:** venue admin accounts via `venue_admins` table (already exists)

### 1.13 Admin Tools
**What it does:** Sway super-admin can create places, communities, events, manage QR codes, view system health.  
**Key tables:** `admin_users` (or use existing email-gated super-admin logic)

### 1.14 Validation / Trust Layer
**What it does:** Determines if a session is real. Phase 0–2: dwell-time threshold (session open for X minutes before auto-close as completed). Phase 6: NFC/geofence/Wallet confirm.  
**Key tables:** `session_validation_events`  
**Fields:** session_id, event_type (scan_open/scan_close/dwell_complete/geo_confirm/nfc_confirm/staff_confirm/auto_expired/flagged_suspicious), occurred_at, metadata_json

---

## 2. Database Schema

### Guiding principles
- `check_ins` = raw input log. No credit.
- `presence_sessions` = the source of truth for participation.
- `user_global_stats` and `user_node_stats` = materialized/computed rollups. Updated by triggers after session completion.
- Rename/repurpose `venues` → `places` via new table + migration (do not drop venues — existing foreign keys).
- All timestamps in UTC. Eastern timezone conversion happens in application layer.

---

### Table: `student_profiles` (existing — alter)
Primary user identity record.

```sql
-- Existing columns to KEEP:
-- id, email, full_name, student_id, created_at, updated_at

-- ADD these columns:
ALTER TABLE public.student_profiles
  ADD COLUMN IF NOT EXISTS display_name text,
  ADD COLUMN IF NOT EXISTS avatar_url text,
  ADD COLUMN IF NOT EXISTS class_year integer,
  ADD COLUMN IF NOT EXISTS campus text DEFAULT 'endicott',
  ADD COLUMN IF NOT EXISTS bio text,
  ADD COLUMN IF NOT EXISTS is_test_account boolean DEFAULT false,
  ADD COLUMN IF NOT EXISTS onboarding_complete boolean DEFAULT false;

-- REMOVE (or nullify) these columns after migration:
-- points, level (replaced by user_global_stats)
```

---

### Table: `places`
Physical locations. Replaces and extends `venues`.

```sql
CREATE TABLE public.places (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  legacy_venue_id uuid REFERENCES public.venues(id),  -- backfill from venues
  name text NOT NULL,
  slug text UNIQUE NOT NULL,
  type text NOT NULL CHECK (type IN ('bar', 'gym', 'event_space', 'academic', 'outdoor', 'restaurant', 'club_room')),
  campus text,
  address text,
  node_code text UNIQUE,           -- QR scan code (replaces venues.check_in_code)
  nfc_tag_id text,                 -- future NFC
  geofence_lat numeric(10, 7),
  geofence_lng numeric(10, 7),
  geofence_radius_meters integer DEFAULT 100,
  active boolean DEFAULT true,
  session_completion_minutes integer DEFAULT 30,  -- dwell threshold
  operator_user_id uuid REFERENCES auth.users(id),
  created_at timestamptz DEFAULT now(),
  updated_at timestamptz DEFAULT now()
);
```

**Seed data:** Insert Gully's with `legacy_venue_id = 'fc8a0103-b2ab-41dc-aa83-efaa16958301'` and correct `session_completion_minutes` (suggest 45 min for a bar).

---

### Table: `communities`
Groups that exist independent of a place.

```sql
CREATE TABLE public.communities (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  name text NOT NULL,
  slug text UNIQUE NOT NULL,
  type text NOT NULL CHECK (type IN ('club', 'team', 'program', 'class', 'campus', 'greek', 'intramural')),
  campus text,
  description text,
  admin_user_id uuid REFERENCES auth.users(id),
  active boolean DEFAULT true,
  created_at timestamptz DEFAULT now()
);

CREATE TABLE public.community_members (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  community_id uuid NOT NULL REFERENCES public.communities(id) ON DELETE CASCADE,
  user_id uuid NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  role text DEFAULT 'member' CHECK (role IN ('member', 'officer', 'admin')),
  joined_at timestamptz DEFAULT now(),
  UNIQUE (community_id, user_id)
);
```

---

### Table: `events`
Time-bounded participation windows. Hosted by a place and/or community.

```sql
CREATE TABLE public.events (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  title text NOT NULL,
  description text,
  place_id uuid REFERENCES public.places(id),
  community_id uuid REFERENCES public.communities(id),
  start_at timestamptz NOT NULL,
  end_at timestamptz NOT NULL,
  completion_window_minutes integer DEFAULT 60,  -- overrides place default for this event
  status text DEFAULT 'draft' CHECK (status IN ('draft', 'active', 'closed')),
  session_count integer DEFAULT 0,   -- running tally, updated by trigger
  created_by uuid REFERENCES auth.users(id),
  created_at timestamptz DEFAULT now(),
  updated_at timestamptz DEFAULT now()
);
```

---

### Table: `check_ins`
Raw scan log. INPUT ONLY. No credit happens here.

```sql
-- Alter existing check_ins table
-- Current columns: id, user_id, venue_id, points_earned, source, checked_in_at

ALTER TABLE public.check_ins
  ADD COLUMN IF NOT EXISTS place_id uuid REFERENCES public.places(id),
  ADD COLUMN IF NOT EXISTS event_id uuid REFERENCES public.events(id),
  ADD COLUMN IF NOT EXISTS session_id uuid,   -- FK added after presence_sessions exists
  ADD COLUMN IF NOT EXISTS client_ip inet,
  ADD COLUMN IF NOT EXISTS device_hint text;

-- points_earned should be set to 0 going forward — field kept for legacy read queries
-- venue_id kept for backward compatibility
```

---

### Table: `presence_sessions`
The core primitive. Source of truth for all participation credit.

```sql
CREATE TABLE public.presence_sessions (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id uuid NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  place_id uuid REFERENCES public.places(id),
  event_id uuid REFERENCES public.events(id),
  community_id uuid REFERENCES public.communities(id),  -- if event has community
  check_in_id uuid REFERENCES public.check_ins(id),    -- the scan that opened this
  opened_at timestamptz NOT NULL DEFAULT now(),
  closed_at timestamptz,
  status text NOT NULL DEFAULT 'open'
    CHECK (status IN ('open', 'completed', 'incomplete', 'suspicious', 'expired')),
  completion_method text
    CHECK (completion_method IN ('dwell_timer', 'second_scan', 'event_window', 'nfc_confirm', 'geo_confirm', 'wallet_confirm', 'staff_confirm', 'auto_expired')),
  participation_credits_issued boolean DEFAULT false,
  credits_issued_at timestamptz,
  notes text,
  created_at timestamptz DEFAULT now()
);

CREATE INDEX idx_presence_sessions_user_id ON public.presence_sessions (user_id);
CREATE INDEX idx_presence_sessions_place_id ON public.presence_sessions (place_id);
CREATE INDEX idx_presence_sessions_status ON public.presence_sessions (status);
CREATE INDEX idx_presence_sessions_opened_at ON public.presence_sessions (opened_at DESC);
```

---

### Table: `session_validation_events`
Every signal that affects a session's status. Audit trail for the completion engine.

```sql
CREATE TABLE public.session_validation_events (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  session_id uuid NOT NULL REFERENCES public.presence_sessions(id) ON DELETE CASCADE,
  event_type text NOT NULL CHECK (event_type IN (
    'scan_open',
    'scan_close',
    'dwell_complete',
    'geo_confirm',
    'nfc_confirm',
    'wallet_confirm',
    'staff_confirm',
    'auto_expired',
    'flagged_suspicious',
    'manual_override'
  )),
  occurred_at timestamptz NOT NULL DEFAULT now(),
  source text,          -- 'system', 'user', 'staff', 'admin'
  metadata jsonb        -- optional: {lat, lng, nfc_uid, staff_id, etc.}
);

CREATE INDEX idx_session_validation_session_id ON public.session_validation_events (session_id);
```

---

### Table: `user_node_stats`
Per-user, per-place participation record. Updated by trigger when session completes.

```sql
CREATE TABLE public.user_node_stats (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id uuid NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  place_id uuid REFERENCES public.places(id),
  community_id uuid REFERENCES public.communities(id),
  node_type text NOT NULL CHECK (node_type IN ('place', 'community')),
  total_completed_sessions integer DEFAULT 0,
  total_incomplete_sessions integer DEFAULT 0,
  first_session_at timestamptz,
  last_session_at timestamptz,
  current_streak_days integer DEFAULT 0,
  longest_streak_days integer DEFAULT 0,
  is_regular boolean DEFAULT false,    -- computed: total_completed_sessions >= 5
  UNIQUE (user_id, place_id),
  UNIQUE (user_id, community_id)
);

CREATE INDEX idx_user_node_stats_user_id ON public.user_node_stats (user_id);
CREATE INDEX idx_user_node_stats_place_id ON public.user_node_stats (place_id);
```

---

### Table: `user_global_stats`
Cross-node participation summary per user. Updated by trigger when session completes.

```sql
CREATE TABLE public.user_global_stats (
  user_id uuid PRIMARY KEY REFERENCES auth.users(id) ON DELETE CASCADE,
  total_completed_sessions integer DEFAULT 0,
  total_incomplete_sessions integer DEFAULT 0,
  distinct_places_visited integer DEFAULT 0,
  distinct_communities integer DEFAULT 0,
  distinct_events_attended integer DEFAULT 0,
  current_tier text DEFAULT 'newcomer'
    CHECK (current_tier IN ('newcomer', 'familiar', 'regular', 'known', 'embedded')),
  tier_updated_at timestamptz,
  first_session_at timestamptz,
  last_session_at timestamptz,
  updated_at timestamptz DEFAULT now()
);
```

---

### Table: `sway_cards`
User identity credential. One per user.

```sql
CREATE TABLE public.sway_cards (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id uuid UNIQUE NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  card_number text UNIQUE NOT NULL,   -- formatted: SWAY-XXXX-XXXX
  tier text DEFAULT 'newcomer',
  total_sessions integer DEFAULT 0,  -- mirrors user_global_stats
  active_node_count integer DEFAULT 0,
  issued_at timestamptz DEFAULT now(),
  last_updated_at timestamptz DEFAULT now(),
  wallet_pass_url text,              -- Apple Wallet (Phase 6)
  wallet_pass_issued_at timestamptz
);
```

---

### Table: `circles`
Private friend/group social layer. Phase 3+.

```sql
CREATE TABLE public.circles (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  name text NOT NULL,
  created_by uuid NOT NULL REFERENCES auth.users(id),
  invite_code text UNIQUE DEFAULT substring(gen_random_uuid()::text, 1, 8),
  is_private boolean DEFAULT true,
  created_at timestamptz DEFAULT now()
);

CREATE TABLE public.circle_members (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  circle_id uuid NOT NULL REFERENCES public.circles(id) ON DELETE CASCADE,
  user_id uuid NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  role text DEFAULT 'member' CHECK (role IN ('member', 'admin')),
  joined_at timestamptz DEFAULT now(),
  UNIQUE (circle_id, user_id)
);
```

---

### Table: `recaps`
Generated participation summaries. Phase 4+.

```sql
CREATE TABLE public.recaps (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id uuid NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  recap_type text NOT NULL CHECK (recap_type IN ('weekly', 'monthly', 'semester')),
  period_start date NOT NULL,
  period_end date NOT NULL,
  data_json jsonb NOT NULL,   -- {total_sessions, top_place, top_event, streak, highlights[]}
  generated_at timestamptz DEFAULT now(),
  UNIQUE (user_id, recap_type, period_start)
);
```

---

### Table: `venue_dashboards` / Operator Config
Thin config record per place operator. Data comes from querying sessions.

```sql
CREATE TABLE public.operator_configs (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  place_id uuid UNIQUE NOT NULL REFERENCES public.places(id) ON DELETE CASCADE,
  operator_user_id uuid NOT NULL REFERENCES auth.users(id),
  dashboard_enabled boolean DEFAULT true,
  notify_on_regular boolean DEFAULT true,  -- ping when user hits 5+ sessions
  regular_threshold integer DEFAULT 5,
  created_at timestamptz DEFAULT now()
);
```

---

### Table: `admin_users`
Super-admin registry. Gate with email check or this table.

```sql
CREATE TABLE public.admin_users (
  user_id uuid PRIMARY KEY REFERENCES auth.users(id) ON DELETE CASCADE,
  email text NOT NULL,
  role text DEFAULT 'admin' CHECK (role IN ('admin', 'super_admin')),
  created_at timestamptz DEFAULT now()
);
```

---

### Trigger: auto-update stats on session completion

```sql
CREATE OR REPLACE FUNCTION public.handle_session_completion()
RETURNS TRIGGER AS $$
BEGIN
  -- Only fire when status transitions TO 'completed'
  IF NEW.status = 'completed' AND OLD.status <> 'completed' THEN
    -- Upsert user_node_stats
    INSERT INTO public.user_node_stats (user_id, place_id, node_type, total_completed_sessions, first_session_at, last_session_at)
    VALUES (NEW.user_id, NEW.place_id, 'place', 1, NEW.opened_at, NEW.opened_at)
    ON CONFLICT (user_id, place_id) DO UPDATE SET
      total_completed_sessions = user_node_stats.total_completed_sessions + 1,
      last_session_at = NEW.opened_at,
      is_regular = (user_node_stats.total_completed_sessions + 1) >= 5;

    -- Upsert user_global_stats
    INSERT INTO public.user_global_stats (user_id, total_completed_sessions, first_session_at, last_session_at)
    VALUES (NEW.user_id, 1, NEW.opened_at, NEW.opened_at)
    ON CONFLICT (user_id) DO UPDATE SET
      total_completed_sessions = user_global_stats.total_completed_sessions + 1,
      last_session_at = NEW.opened_at,
      updated_at = now();

    -- Recompute tier
    UPDATE public.user_global_stats SET
      current_tier = CASE
        WHEN total_completed_sessions >= 30 THEN 'embedded'
        WHEN total_completed_sessions >= 15 THEN 'known'
        WHEN total_completed_sessions >= 7  THEN 'regular'
        WHEN total_completed_sessions >= 3  THEN 'familiar'
        ELSE 'newcomer'
      END,
      tier_updated_at = now()
    WHERE user_id = NEW.user_id;

    -- Update sway_card
    UPDATE public.sway_cards SET
      tier = (SELECT current_tier FROM public.user_global_stats WHERE user_id = NEW.user_id),
      total_sessions = (SELECT total_completed_sessions FROM public.user_global_stats WHERE user_id = NEW.user_id),
      last_updated_at = now()
    WHERE user_id = NEW.user_id;

    -- Mark credits issued on session
    NEW.participation_credits_issued = true;
    NEW.credits_issued_at = now();
  END IF;
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trg_session_completion
BEFORE UPDATE ON public.presence_sessions
FOR EACH ROW EXECUTE FUNCTION public.handle_session_completion();
```

---

## 3. Completion Engine Design

### The flow: tap → session → completion → credit

```
User scans QR
    ↓
check_ins INSERT (raw log, no credit)
    ↓
presence_sessions INSERT (status = 'open', opened_at = now())
    ↓
session_validation_events INSERT (event_type = 'scan_open')
    ↓
[wait for completion signal]
    ↓
One of these closes the session:
  A. Dwell timer fires (session open for X min, no anomaly)
  B. User scans again at same place (second_scan)
  C. Event window closes (end_at passes)
  D. NFC/geo/wallet confirm (Phase 6)
  E. Staff confirms (manual override)
    ↓
presence_sessions UPDATE (status = 'completed', completion_method = ...)
    ↓
session_validation_events INSERT (event_type = 'dwell_complete' or equivalent)
    ↓
trigger fires → user_node_stats + user_global_stats + sway_cards UPDATE
    ↓
Credit issued.
```

### Dwell timer (Phase 1 default completion method)

**Mechanism:** A Supabase Edge Function `close-open-sessions` runs on a cron job every 5 minutes. It finds sessions that have been open for ≥ `place.session_completion_minutes` and closes them as `completed`.

```typescript
// Pseudocode for close-open-sessions edge function
const cutoff = new Date(Date.now() - place.session_completion_minutes * 60 * 1000);

const openSessions = await supabase
  .from('presence_sessions')
  .select('id, user_id, place_id, opened_at')
  .eq('status', 'open')
  .lte('opened_at', cutoff.toISOString());

for (const session of openSessions) {
  await supabase
    .from('presence_sessions')
    .update({ status: 'completed', closed_at: now, completion_method: 'dwell_timer' })
    .eq('id', session.id);

  await supabase.from('session_validation_events').insert({
    session_id: session.id,
    event_type: 'dwell_complete',
    source: 'system',
    metadata: { closed_at_minutes: minutesSinceOpen }
  });
}
```

### Suspicious session detection

A session is flagged `suspicious` if:
- Opened and check-in occurred < 60 seconds ago AND user has already completed a session at this place within the last 2 hours (rapid re-entry)
- More than 3 open sessions for the same user at the same place on the same day (QR farming)
- Session opened at a time when the venue is known to be closed (future: venue hours table)

When suspicious: set `status = 'suspicious'`. No credit issued. Log to `session_validation_events`. Does NOT ban user — just doesn't credit.

### Incomplete session

A session closes as `incomplete` if:
- The session timer runs for more than 4× `session_completion_minutes` with no additional confirmation signal (user left without completing)
- This is the edge case where someone scanned, immediately left, and the session sat open. After 4× threshold → mark expired/incomplete, no credit.

### Key rules enforced by the engine

1. Only ONE open session per user per place at a time. If a new scan comes in while one is open, close the old one as `scan_close` and open a new one (or treat as second-scan completion of the first).
2. Points/status are NEVER updated in `qr-checkin` or any scan function. Only the `handle_session_completion` trigger updates stats.
3. `check_ins.points_earned` should be set to `0` for all new records going forward.

---

## 4. Product Roadmap

### Phase 0 — Clean Gully's Flow (2–3 weeks)
Goal: Remove legacy noise. Stabilize what's live. No new features.

- Remove instant points award from `qr-checkin`
- Remove MugClub references from UI (archive, don't delete)
- Remove public leaderboard from student-facing pages
- Remove payments/rewards references from UI
- Remove raffle, drink winner, launch blast components from main flows
- Keep check-in QR flow working exactly as-is
- Add `places` table, seed Gully's, link `place_id` to existing check-ins
- Add `presence_sessions` table (start logging sessions, no credit yet)
- Add `session_validation_events` table

**Success metric:** Gully's QR check-in works. Sessions are being logged. No crashes.

---

### Phase 1 — Completion Sessions (3–4 weeks)
Goal: Sessions close. Credit is issued after dwell. Existing users see their session count.

- Deploy `close-open-sessions` edge function with cron (pg_cron every 5 min)
- Build `handle_session_completion` trigger
- Add `user_global_stats` and `user_node_stats` tables + seed from existing check_ins
- Add `sway_cards` table, generate card for every existing user
- Update `Profile.tsx` to show session count from `user_global_stats` (not points)
- Replace "X points" with "X sessions completed" everywhere
- Add tier label (Newcomer / Familiar / Regular / Known / Embedded) to profile
- Add basic suspicious session detection

**Success metric:** Sessions complete via dwell timer. Stats update. Card shows real data.

---

### Phase 2 — Sway Card (2–3 weeks)
Goal: Users have a visible identity credential that feels premium.

- Build `SwayCard.tsx` component — dark card, name, tier, session count, node count
- Build `/card` route — full-screen card view, tap to flip for stats
- Add card animation (Framer Motion flip)
- Replace current check-in success screen with "You showed up" confirmation + card update animation
- Build `/profile` around card as centerpiece (not points/leaderboard)
- Add "share your card" (screenshot prompt — no external API needed)

**Success metric:** Card looks like a credential. Check-in confirmation feels meaningful.

---

### Phase 3 — Multi-Node Campus Graph (4–6 weeks)
Goal: Gully's + campus gym + Foundry/Angle Center + 1 event-only node all on Sway.

- Add `communities` + `community_members` tables
- Add `events` table (replaces/extends `venue_events`)
- Create place nodes: campus gym, Foundry room, Entrepreneurship Club event node
- Generate unique QR codes per place
- Build admin tool to create place + generate QR
- Update check-in flow to route to `place_id` not `venue_id`
- Add `user_node_stats` per-place stats to profile
- Add `/nodes` page — map of campus nodes user has visited (list, not map yet)
- Build event check-in flow: scan event QR → session opens with `event_id`

**Success metric:** Students can check in at 3+ distinct campus nodes. Stats track across all.

---

### Phase 4 — Timeline + Recaps (3–4 weeks)
Goal: Users can see their personal participation story.

- Build `/timeline` page — reverse-chronological completed sessions
- Each card: place name, event title (if any), date, session duration
- Build weekly recap generation (Supabase Edge Function, triggered Friday night)
- Build `/recap/[id]` page — shareable weekly summary card
- Add "Your Sway Story" section to profile — first check-in date, total nodes, total sessions, longest streak

**Success metric:** Students open timeline and say "this is my semester."

---

### Phase 5 — Operator Dashboard (2–3 weeks)
Goal: Gully's operator can log in and see participation signal.

- Build `/dashboard` route (gated by `venue_admins` or `operator_configs`)
- Dashboard tabs: Overview, Visitors, Events, Trends
- Overview: total unique visitors this week, return rate, new vs returning
- Visitors: list of sessions with name, session count, last visit, regular badge
- Events: which events ran, how many sessions, post-event return rate
- Trends: day/time heatmap, 7/14/30-day return windows
- Build CSV export for operator (sessions this month)

**Success metric:** Gully's owner opens dashboard and learns something actionable.

---

### Phase 6 — Stronger Validation (Post-Fall Launch)
Goal: Move from QR-only ("logged presence") to multi-signal ("validated presence").

- NFC tag scan (Web NFC API on Android, future)
- GPS geofence confirmation (background location permission required)
- Apple Wallet pass check-in (PassKit)
- Device session trust (fingerprint repeat user with same device = lower suspicion score)
- Second-scan completion (scan again on exit)

**Not in scope until Phase 5 is stable and Gully's has 3+ nodes live.**

---

## 5. User Experience Flows

### Flow 1: First-Time Student Signup
```
Student lands on scan URL (sway.link/gullys or QR)
  → If not logged in: redirect to /auth?redirect=checkin&venue=gullys
  → Auth page: "Sign in to Sway" — name, email, password (or magic link)
  → On success: create student_profile + user_global_stats + sway_cards record
  → Redirect to check-in flow
  → Check-in completes (session opens)
  → Show: "You're in. Sway remembers." — first-time welcome card
  → Brief onboarding: swipe through 3 cards (what Sway is, your card, come back)
  → Land on /profile — show new Sway Card
```

**DB changes:** `student_profiles` INSERT, `user_global_stats` INSERT, `sway_cards` INSERT, `check_ins` INSERT, `presence_sessions` INSERT

---

### Flow 2: Returning Student Check-in at Gully's
```
Student opens sway.link/gullys or scans QR at Gully's
  → Already logged in: goes directly to check-in
  → qr-checkin function fires:
      - INSERT check_ins (source='qr')
      - INSERT presence_sessions (status='open')
      - INSERT session_validation_events (scan_open)
  → Show: "You're in. Session started." — "We'll credit this once you've been here a while."
  → User goes about their night
  → [35 min later] close-open-sessions cron fires
      - UPDATE presence_sessions SET status='completed', completion_method='dwell_timer'
      - trigger: update user_node_stats, user_global_stats, sway_cards
  → Next time user opens app: notification/card shows updated session count
```

**Key UX:** Check-in confirmation does NOT say "you earned X points." It says "Session started" or "You showed up."

---

### Flow 3: Event Check-in (Trivia Night)
```
Operator creates event in admin: "Trivia Night" at Gully's, start 7PM, end 10PM
  → Event published → new event QR generated (or same place QR with event_id context)
Student scans QR:
  → qr-checkin detects active event at this place
  → Show: "Trivia Night is live. Check in to this event?" [Yes / No]
  → On Yes: INSERT check_ins with event_id, INSERT presence_sessions with event_id + place_id
  → Session completion_window = event.end_at (10PM) — event window closes session
  → At 10PM: close-open-sessions marks sessions with this event_id as completed
  → Stats update: event_id credited to user's timeline
```

---

### Flow 4: Sports Game Attendance
```
Operator creates event: "Soccer vs. Nichols" at outdoor node, 2-hour window
  → QR posted at stadium entrance
Student scans:
  → Opens session tagged to this event + place
  → Completion: event window (2 hours) or dwell timer (45 min), whichever comes first
  → Session completes → user's card shows +1 session, event appears in timeline
```

---

### Flow 5: Gym Check-in
```
Gym has its own place node. QR posted at gym entrance.
Student scans:
  → Opens session (status=open)
  → Dwell timer = 30 minutes (gym sessions shorter than bar)
  → session_completion_minutes configured on places row for gym = 30
  → Close-open-sessions runs → marks complete after 30 min
  → User's timeline shows: "Campus Gym — Session" with date
```

---

### Flow 6: Viewing Your Sway Card
```
User taps "My Card" or navigates to /card
  → Full-screen dark card renders
  → Shows: name, class year, tier badge, total sessions, active node count
  → Tap card: flip animation → back shows per-node breakdown
  → Share button: triggers native share with card screenshot (no external upload)
```

---

### Flow 7: Viewing Personal Timeline
```
User navigates to /timeline (or Profile → Timeline tab)
  → Reverse-chronological list of presence_sessions WHERE status='completed'
  → Each card shows:
      - Place name + icon
      - Event name (if event_id)
      - Date + approximate duration
      - "Session completed" label
  → Infinite scroll or paginated (20 per page)
  → Empty state: "Your story is just starting. Check in somewhere."
```

---

### Flow 8: Operator Viewing Dashboard
```
Operator logs in at /dashboard
  → Sees their linked place(s)
  → Overview card: unique visitors this week, return rate, total sessions
  → Visitor list: sorted by total sessions (regulars first)
  → Each visitor row: first name, last initial, session count, last visit, tier badge
  → Events tab: list of events, session count per event, post-event 7-day return rate
  → Trend chart: day/hour heatmap from presence_sessions grouped by day_of_week + hour
```

---

### Flow 9: Admin Creating a New Node / Event
```
Sway admin logs in at /admin
  → Places tab → New Place form: name, type, campus, session_completion_minutes
  → System generates unique node_code (SWAY_NODENAME_XXXXXX)
  → Admin downloads QR code image for that node_code
  → Admin prints and posts QR at location
  → Place is live. Students can scan.

Events:
  → Events tab → New Event form: title, place, start_at, end_at
  → System creates event record, links to place
  → Admin publishes event → active_events query picks it up during check-in
```

---

## 6. UI/UX Direction

### Reference aesthetic
Apple Wallet · WHOOP · Strava · A passport · A membership credential

### Not the reference
Punch card · Stamp card · Gamified badge wall · Coupon app · Leaderboard screen

### Principles applied to code

**Colors:**
```
Background: #0A0A0A (near-black)
Card: #141414
Surface: #1A1A1A
Border: #2A2A2A
Text primary: #FFFFFF
Text secondary: #888888
Accent: #E0FF4F (electric yellow-green — or brand color)
Tier: tier-specific glow colors (newcomer: gray, familiar: blue, regular: green, known: gold, embedded: white)
```

**Typography:** Large, confident. No small text. Session count = large number, not small badge.

**Check-in confirmation screen:**
- Dark fullscreen takeover
- Large "You showed up." text
- Subtle pulse animation
- Place name
- "Session started — come back soon." subtext
- NOT: "You earned X points!" NOT: "Level up!" NOT: confetti

**Sway Card component:**
- 3:2 ratio dark card (like a hotel key or transit card)
- User name top-left
- Tier badge top-right
- Large session count center
- Campus + class year bottom
- Subtle gradient or grain texture
- Card flip (Framer Motion `rotateY`) reveals per-node stats on back

**Session completion (async — next app open):**
- Show badge-style notification: "Session completed at Gully's"
- Not a pop-up. A quiet card in the notification/activity feed.

**No:**
- Points totals on main screens
- Leaderboards anywhere
- Countdown timers to next reward
- Level-up animations tied to individual taps
- Stars, badges, coins imagery

---

## 7. Operator Dashboard — Query Specifications

### Overview metrics
```sql
-- Unique visitors this week
SELECT COUNT(DISTINCT user_id) 
FROM presence_sessions 
WHERE place_id = $place_id AND status = 'completed'
  AND opened_at >= now() - interval '7 days';

-- Return rate: % of users with 2+ completed sessions
SELECT 
  COUNT(*) FILTER (WHERE session_count >= 2)::float / COUNT(*) AS return_rate
FROM (
  SELECT user_id, COUNT(*) as session_count 
  FROM presence_sessions 
  WHERE place_id = $place_id AND status = 'completed'
  GROUP BY user_id
) t;

-- New vs returning this week
SELECT 
  is_returning,
  COUNT(*) as visitor_count
FROM (
  SELECT user_id,
    (first_session_at < now() - interval '7 days') as is_returning
  FROM user_node_stats
  WHERE place_id = $place_id
) t GROUP BY is_returning;
```

### Visitor list
```sql
SELECT 
  sp.full_name,
  uns.total_completed_sessions,
  uns.last_session_at,
  uns.is_regular,
  ugs.current_tier
FROM user_node_stats uns
JOIN student_profiles sp ON sp.id = uns.user_id
JOIN user_global_stats ugs ON ugs.user_id = uns.user_id
WHERE uns.place_id = $place_id
ORDER BY uns.total_completed_sessions DESC, uns.last_session_at DESC;
```

### Event-to-return tracking
```sql
-- Did people who attended trivia night return within 14 days?
WITH event_attendees AS (
  SELECT DISTINCT user_id 
  FROM presence_sessions 
  WHERE event_id = $event_id AND status = 'completed'
)
SELECT 
  COUNT(*) as attendees,
  COUNT(*) FILTER (
    WHERE EXISTS (
      SELECT 1 FROM presence_sessions ps2
      WHERE ps2.user_id = ea.user_id 
        AND ps2.place_id = $place_id
        AND ps2.event_id IS NULL  -- non-event return
        AND ps2.status = 'completed'
        AND ps2.opened_at > (SELECT MAX(opened_at) FROM presence_sessions WHERE event_id = $event_id)
        AND ps2.opened_at < (SELECT MAX(opened_at) FROM presence_sessions WHERE event_id = $event_id) + interval '14 days'
    )
  ) as returned_within_14_days
FROM event_attendees ea;
```

### Day/hour heatmap
```sql
SELECT 
  EXTRACT(DOW FROM opened_at AT TIME ZONE 'America/New_York') as day_of_week,
  EXTRACT(HOUR FROM opened_at AT TIME ZONE 'America/New_York') as hour_of_day,
  COUNT(*) as session_count
FROM presence_sessions
WHERE place_id = $place_id AND status = 'completed'
  AND opened_at >= now() - interval '30 days'
GROUP BY day_of_week, hour_of_day
ORDER BY day_of_week, hour_of_day;
```

---

## 8. Engineering Tickets

---

### TICKET-001: Remove instant points from check-in
**Priority:** P0 — do this first  
**Goal:** Stop awarding `points_earned` on `check_ins` insert. The old system credits immediately; the new system credits only on session completion.  
**Files affected:**
- `supabase/functions/qr-checkin/index.ts` — set `points_earned = 0` on all new check_in inserts; remove `student_profiles.points` update logic entirely
- `supabase/functions/log-tap/index.ts` — remove points logic
- `supabase/functions/update-tap/index.ts` — remove points update
**DB changes:** None (schema unchanged). All new check_ins get `points_earned = 0`.  
**Acceptance criteria:**
- Student scans QR → `check_ins` row created with `points_earned = 0`
- `student_profiles.points` is NOT updated
- Check-in confirmation still shows (can still say "Checked in")
- No console errors
**Edge cases:** Legacy check-ins with `points_earned > 0` remain — do not touch historical data.

---

### TICKET-002: Add places table and seed Gully's
**Priority:** P0  
**Goal:** Create `places` table. Seed Gully's as the first place node. Link existing `venues.id` via `legacy_venue_id`.  
**Files affected:**
- New migration file in `supabase/migrations/`
**DB changes:** CREATE TABLE places, INSERT Gully's record with `legacy_venue_id = 'fc8a0103-b2ab-41dc-aa83-efaa16958301'`, `session_completion_minutes = 45`, `node_code = 'SWAY_GULLYS_V1'`  
**Acceptance criteria:**
- `places` table exists
- Gully's row exists with correct fields
- Can query `SELECT * FROM places WHERE slug = 'gullys'` and get one row
**Edge cases:** Do not delete or alter `venues` table — `check_ins.venue_id` still references it.

---

### TICKET-003: Add presence_sessions and session_validation_events tables
**Priority:** P0  
**Goal:** Create the core session primitive tables.  
**Files affected:** New migration file  
**DB changes:** CREATE TABLE presence_sessions, CREATE TABLE session_validation_events, CREATE INDEX statements, CREATE TRIGGER `trg_session_completion`  
**Acceptance criteria:**
- Tables exist with correct schema
- Trigger fires when `presence_sessions.status` updates to 'completed'
- `user_global_stats` and `user_node_stats` rows created/updated on trigger

---

### TICKET-004: Add user_global_stats, user_node_stats, sway_cards tables
**Priority:** P0 (needed by TICKET-003 trigger)  
**Files affected:** New migration file  
**DB changes:** CREATE TABLE user_global_stats, CREATE TABLE user_node_stats, CREATE TABLE sway_cards  
**Acceptance criteria:**
- Tables exist
- Backfill script seeds `user_global_stats` for all existing `student_profiles`
- `sway_cards` generates one row per user with card_number format `SWAY-XXXX-XXXX`

---

### TICKET-005: Update qr-checkin to create presence_session
**Priority:** P1  
**Goal:** After inserting `check_ins`, also INSERT a `presence_sessions` row with `status='open'` and INSERT a `session_validation_events` row with `event_type='scan_open'`.  
**Files affected:** `supabase/functions/qr-checkin/index.ts`  
**DB changes:** None (tables from TICKET-003)  
**Acceptance criteria:**
- Scan at Gully's → `check_ins` row created + `presence_sessions` row (status=open) created + `session_validation_events` row (scan_open) created
- If user already has an open session at this place today: close old session as 'scan_close' before opening new one
**Edge cases:** Utility venue (gym) path already has separate logic — keep it, or migrate it to same session flow later.

---

### TICKET-006: Deploy close-open-sessions Edge Function + cron
**Priority:** P1  
**Goal:** Runs every 5 minutes. Closes all `presence_sessions WHERE status='open'` that have been open ≥ `places.session_completion_minutes`. Marks `status='completed'`, `completion_method='dwell_timer'`.  
**Files affected:** New `supabase/functions/close-open-sessions/index.ts`  
**DB changes:** pg_cron extension enabled, cron job added  
**Acceptance criteria:**
- Open sessions older than `session_completion_minutes` close as completed
- Trigger fires → stats update
- Sessions open for < threshold NOT closed
- Suspicious detection: flag sessions from user with 3+ completions at same place same day
**Edge cases:** Session with `event_id` should use `events.end_at` as completion trigger if event already ended, even if dwell timer hasn't fired.

---

### TICKET-007: Update Profile page to show session stats
**Priority:** P1  
**Goal:** Replace points/level display with session count, tier, and Sway Card.  
**Files affected:** `src/pages/Profile.tsx`, `src/components/SwayCard.tsx`  
**DB changes:** None (reads from `user_global_stats`, `sway_cards`)  
**Acceptance criteria:**
- Profile shows: tier badge, total completed sessions, distinct places visited
- No "points" label visible on profile page
- SwayCard component renders with correct tier color
**Edge cases:** User with 0 sessions: show "Newcomer" tier, session count = 0.

---

### TICKET-008: Build Sway Card component and /card route
**Priority:** P2  
**Goal:** Premium identity credential. Dark card with name, tier, session count. Flip animation reveals per-node stats.  
**Files affected:** `src/components/SwayCard.tsx` (update), `src/pages/Profile.tsx`, new route `/card`  
**DB changes:** None  
**Acceptance criteria:**
- Card renders at /card with user data
- Framer Motion flip on tap (Y-axis rotation, 180°)
- Front: name, tier badge, total sessions, active nodes
- Back: list of nodes with session count each
- Share button: `navigator.share()` with card screenshot
**Edge cases:** Share not supported on desktop → show "Copy link" fallback.

---

### TICKET-009: Build admin place/event creation tool
**Priority:** P2  
**Goal:** Super-admin can create place nodes and events. QR code generated.  
**Files affected:** `src/pages/SuperAdmin.tsx` (update), new component `src/components/admin/PlacesTab.tsx`, new component `src/components/admin/EventsTab.tsx` (update)  
**DB changes:** INSERT into `places`, INSERT into `events`  
**Acceptance criteria:**
- Admin creates place → `node_code` generated → QR code image displayed for download
- Admin creates event → linked to place, with start_at/end_at, status=draft → publish button
- Published event appears in active event check during scan window
**Edge cases:** Event with no place_id (community-only event) — allow community_id only.

---

### TICKET-010: Build events table and campus nodes (gym, Foundry)
**Priority:** P3  
**Goal:** Add `events` table. Add place nodes for campus gym + Foundry/Angle Center.  
**Files affected:** New migration file, admin tool (TICKET-009)  
**DB changes:** CREATE TABLE events (replaces/extends venue_events), INSERT new places  
**Acceptance criteria:**
- Gym place node exists with `session_completion_minutes = 30`
- Foundry place node exists
- New events can be created against these places
- Event check-in flow works for all nodes
**Edge cases:** Existing `venue_events` data — do NOT delete, keep for read queries on history.

---

### TICKET-011: Build /timeline page
**Priority:** P4  
**Goal:** Reverse-chronological list of user's completed sessions.  
**Files affected:** `src/pages/Activity.tsx` (repurpose) or new `src/pages/Timeline.tsx`  
**DB changes:** None  
**Query:** `SELECT ps.*, p.name as place_name, e.title as event_title FROM presence_sessions ps LEFT JOIN places p ON p.id = ps.place_id LEFT JOIN events e ON e.id = ps.event_id WHERE ps.user_id = auth.uid() AND ps.status = 'completed' ORDER BY ps.opened_at DESC LIMIT 20`  
**Acceptance criteria:**
- Page loads with completed sessions
- Each card shows place, event (if any), date
- Pagination or infinite scroll
- Empty state if no sessions

---

### TICKET-012: Build operator dashboard
**Priority:** P5  
**Goal:** Venue/community operator sees participation signal.  
**Files affected:** `src/pages/VenueDashboard.tsx` (rebuild)  
**DB changes:** None (reads from presence_sessions, user_node_stats)  
**Tabs:**
- Overview: session count, unique visitors, return rate (7-day)
- Visitors: sorted list with session count, tier, last visit
- Events: per-event session count + 14-day return rate
- Trends: day/hour heatmap
**Acceptance criteria:**
- Dashboard loads for venue_admins
- Data is correct (no test account data)
- CSV export works for visitors list

---

## 9. Guardrails — Do Not Build Yet

These are explicitly blocked until participation memory is proven at scale:

| Blocked Item | Reason |
|---|---|
| Payments / tab management | Phase 6. Proven participation first. |
| Ordering system | Not participation infrastructure. |
| Public leaderboards | Contradicts identity-first thesis. Encourages gaming, not habit. |
| Crypto / token language | Not what this is. |
| Governance / DAO voting | No. |
| Rewards marketplace | Points → goods = loyalty app = wrong direction. |
| Complex staff workflows | Staff must not need to change anything. |
| Heavy POS integrations | POS is transaction layer. Sway is participation layer. |
| Aggressive referral farming | Undermines organic density signal. |
| Discounts-first loyalty | Directly contradicts thesis. |
| AI-generated content | Distraction. Not what creates behavior. |
| Social feed / public posts | Not the product. |
| Push notification spam | Earned attention only. |

---

## 10. Claude / Lovable Implementation Prompts

### Phase 0 Prompt (for coding agent)

```
You are building on a React + Supabase web app called Sway.

CONTEXT: Sway is a participation identity layer for real-world communities. It is NOT a loyalty app or payments app. The current codebase has legacy code from a previous direction (MugClub, points rewards, public leaderboards). We are cleaning this up in Phase 0.

TASK: Remove instant points rewards from the check-in flow.
1. In supabase/functions/qr-checkin/index.ts:
   - Find all `student_profiles.points` UPDATE statements and REMOVE them.
   - Set `points_earned: 0` on all new check_ins INSERT statements.
   - Do NOT change anything else about the check-in flow.
2. Do not touch any UI files yet.
3. Do not delete the points column from student_profiles (legacy data).
4. Run the function locally or confirm changes by reading the file before saving.

The goal is that from now on, scanning a QR code logs the check-in but does not award any points or update any stats. Stats will be handled by a completion engine in Phase 1.

GUARDRAILS: Do not add new features. Do not touch payments. Do not touch MugClub. Only remove instant points.
```

---

### Phase 1 Prompt (for coding agent)

```
You are building on a React + Supabase web app called Sway.

CONTEXT: Sway turns physical presence into identity. The core principle is: Tap = intent, Completion = credit. Do NOT award anything on check-in. Credit is only issued after a "presence session" is marked as completed.

TASK: Implement the completion session system.

1. Run the migration in supabase/migrations/ that creates these tables:
   - places (columns: id, legacy_venue_id, name, slug, type, campus, node_code, session_completion_minutes, active, operator_user_id, created_at)
   - presence_sessions (columns: id, user_id, place_id, event_id, check_in_id, opened_at, closed_at, status, completion_method, participation_credits_issued, credits_issued_at)
   - session_validation_events (columns: id, session_id, event_type, occurred_at, source, metadata jsonb)
   - user_global_stats (columns: user_id PK, total_completed_sessions, distinct_places_visited, current_tier, first_session_at, last_session_at, updated_at)
   - user_node_stats (columns: id, user_id, place_id, total_completed_sessions, first_session_at, last_session_at, is_regular)
   - sway_cards (columns: id, user_id, card_number, tier, total_sessions, active_node_count, issued_at, last_updated_at)

2. Seed Gully's into the places table:
   - legacy_venue_id: 'fc8a0103-b2ab-41dc-aa83-efaa16958301'
   - name: 'Gully's', slug: 'gullys', type: 'bar', campus: 'endicott'
   - node_code: 'SWAY_GULLYS_V1', session_completion_minutes: 45

3. Create a Postgres trigger handle_session_completion that fires BEFORE UPDATE on presence_sessions. When status changes TO 'completed', it must:
   - UPSERT user_node_stats (increment total_completed_sessions for this place)
   - UPSERT user_global_stats (increment total_completed_sessions, recompute tier)
   - UPDATE sway_cards (sync tier, total_sessions)
   - SET participation_credits_issued = true on the session

4. Create Edge Function supabase/functions/close-open-sessions/index.ts that:
   - Queries all presence_sessions WHERE status='open'
   - For each session: look up the place's session_completion_minutes
   - If session.opened_at + completion_minutes < now(): UPDATE status='completed', completion_method='dwell_timer', closed_at=now()
   - INSERT session_validation_events row with event_type='dwell_complete'
   - This function will be called by pg_cron every 5 minutes

5. Update supabase/functions/qr-checkin/index.ts to:
   - After inserting check_ins: look up place_id from places WHERE node_code matches or legacy_venue_id matches venue_id
   - INSERT presence_sessions (status='open', user_id, place_id, check_in_id)
   - INSERT session_validation_events (event_type='scan_open', session_id)
   - If user already has an open session at this place: UPDATE old session status='completed', completion_method='scan_close' first

GUARDRAILS:
- Do NOT award points anywhere.
- Do NOT update student_profiles.points.
- Do NOT build UI in this phase.
- Do NOT add payment tables.
- Presence_sessions status 'completed' is the ONLY trigger for stats updates.
```

---

### Phase 2 Prompt (for coding agent)

```
You are building on a React + Supabase web app called Sway.
Stack: React + Vite + Tailwind + shadcn/ui + Framer Motion + Supabase + TanStack Query

CONTEXT: Sway is an identity-first participation layer. The Sway Card is a user's identity credential — it should feel like an Apple Wallet card or membership card, NOT a loyalty punch card.

TASK: Build the Sway Card UI.

1. Update src/components/SwayCard.tsx:
   - Dark card component (bg #141414, rounded-2xl)
   - Props: { userId, displayName, classYear, tier, totalSessions, activeNodeCount }
   - Front face: name top-left, tier badge top-right (colored by tier), large session count center, "Sway" watermark bottom-right
   - Back face (flip): list of places with session count each
   - Framer Motion: tap/click triggers rotateY 180 animation (use AnimatePresence + motion.div with backfaceVisibility hidden)
   - No points. No coins. No stars.
   - Tier colors: newcomer=gray, familiar=blue-500, regular=green-500, known=yellow-500, embedded=white

2. Create src/pages/Card.tsx route at /card:
   - Full-screen dark background
   - Centered SwayCard component
   - Fetch data from user_global_stats and sway_cards using TanStack Query
   - "Share" button uses navigator.share() with text "Check out my Sway Card"

3. Update src/pages/Profile.tsx:
   - Remove points display
   - Remove level display
   - Remove leaderboard references
   - Add SwayCard component at top
   - Below: tier name + description, total sessions, "Member since [first_session_at]"
   - Link to /timeline (or /activity)
   - Link to /card for full-screen view

4. Update check-in confirmation screen (src/components/CheckInSuccessCard.tsx or equivalent):
   - Message: "You showed up." (large text)
   - Subtext: "Session started at [place name]"
   - Remove any "You earned X points!" text
   - Remove any level-up language

GUARDRAILS:
- No points language anywhere.
- No leaderboard.
- No payment UI.
- Card animation must feel smooth (spring config: stiffness 200, damping 25).
- Data reads from user_global_stats and sway_cards — NOT from student_profiles.points.
```

---

### Phase 5 Prompt (for coding agent)

```
You are building on a React + Supabase web app called Sway.
Stack: React + Vite + Tailwind + shadcn/ui + Supabase + TanStack Query

CONTEXT: Venue operators need to see participation signal. This is a read-only analytics dashboard — no staff workflow changes, no POS, no ordering.

TASK: Build the operator dashboard at /dashboard.

The dashboard is gated by venue_admins table (existing). Operator sees data for their place_id.

DATA QUERIES to implement (Supabase client-side or via RPC):

1. Overview stats:
   - Unique visitors (past 7 days): COUNT(DISTINCT user_id) FROM presence_sessions WHERE place_id=$pid AND status='completed' AND opened_at > now()-7days
   - Return rate: % of all-time visitors with 2+ completed sessions at this place
   - Total sessions this week

2. Visitor list:
   - JOIN user_node_stats + student_profiles + user_global_stats
   - Show: first name, last initial only (privacy), session count, last visit, is_regular badge, tier
   - Sort: session count DESC
   - Limit: 50

3. Event performance:
   - List events linked to this place
   - For each: session count, and post-event 14-day return count

4. Day/hour heatmap:
   - Aggregate presence_sessions by day_of_week + hour_of_day (Eastern timezone)
   - Return as 2D array [day][hour] = count

TABS to build:
- Overview (default)
- Visitors
- Events
- Trends

GUARDRAILS:
- No user full names exposed — first name + last initial only
- No session content visible (just counts and dates)
- No payment data
- No staff workflow features
- No "send message to visitor" feature
- Test accounts (is_test_account = true) excluded from all counts
```

---

## Appendix: What Exists in Current Codebase (Phase 0 reference)

| Existing Item | Status | Action |
|---|---|---|
| `check_ins` table | Keep | Add place_id, event_id columns; set points_earned=0 going forward |
| `venues` table | Keep (for FK compat) | New `places` table maps to it via legacy_venue_id |
| `venue_events` table | Keep | New `events` table maps to it; keep for history |
| `student_profiles` | Keep | Remove points/level from display; keep columns for now |
| `qr-checkin` function | Update | Remove points; add presence_session creation |
| `SwayCard.tsx` component | Rebuild | New design — identity card, not reward card |
| `VenueDashboard.tsx` | Rebuild | Query from presence_sessions not check_ins |
| `VenueLeaderboard.tsx` | Archive | Not in new model |
| MugClub components | Archive | Remove from active routes; keep in codebase |
| `stripe-webhook`, `create-wallet-checkout` etc. | Leave alone | Not touched until Phase 6 |
| `generate-wallet-pass` | Leave alone | Phase 6 |
| `TierRewardsTab`, `UserRewardsTab` | Archive | Remove from admin nav |
| `Referrals.tsx` | Archive | Remove from nav |

---

*Built for Sway Native Layer — Fall 2026 redeployment. Identity-first. Completion-first. Campus-density-first.*

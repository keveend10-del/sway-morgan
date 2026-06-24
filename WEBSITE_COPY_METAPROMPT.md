# Sway Website Copy Metaprompt
**Use:** Paste this into Claude Code (or any AI) inside the `sway-landing` repo to update website copy.
**Rule:** Rewrite words only. Do not change layout, components, design system, colors, fonts, spacing, or section order.

---

## Your Role

You are updating the copy on Sway's landing page. Sway is an early-stage startup. The copy must be strategically precise — not generic SaaS, not nightlife app, not loyalty punch-card.

Read every instruction here before touching a file. Copy decisions have strategic consequences.

---

## What Sway Is (your operating context)

Sway is the check-in and identity layer for real-world social life, starting with campus communities.

**The core insight:** Most apps pull you into the phone. Sway is the opposite.

> Tap once. Put your phone away. Live your life. Sway remembers.

Sway turns going out into memory, status, and identity. Students get a private timeline of places they actually show up, regular status at their favorite spots, Sway Cards, and semester recaps. Venues get lightweight insight into repeat behavior, regulars, and what brings students back — without replacing POS, payments, ticketing, or staff workflows.

**Cultural frame:** Sway is technology for people who want to live more of their life offline — while still getting memory, recognition, and rewards for the real things they do.

**One-line description:** The memory layer for physical life.

**What Sway is NOT:** A loyalty app. A rewards platform. A POS replacement. A payments company. A ticketing platform. A crypto project. A social feed. A generic analytics dashboard. Never imply any of these.

---

## Pilot Data — Use These Numbers Exactly

The Spring 2026 pilot ran at two venues: Gully's bar and the Endicott Gym.

**Gully's-only (the signal — use this when leading):**
- 69 unique users
- 37.7% return rate (students who visited 2+ times)
- 23.2% reached 3+ visits
- 9-week deployment
- Zero paid marketing, zero incentives, zero staff workflow changes

**Combined pilot (Gully's + Endicott Gym — use only when showing total scale):**
- 157 unique users
- ~23% blended return rate
- 5 students visited both venues (3.2% cross-venue)

**CRITICAL — Two numbers are wrong on the current site:**
1. The venues page `VenueProof` section shows: "255 total check-ins, 155 unique students, 81% activation rate, 37% return signal." This blends venues and uses outdated counts. Fix to: lead with Gully's 69 users + 37.7% return rate as the main stat. Move the 81% activation rate to a supporting callout if you keep it.
2. The pilot page `Stats` section leads with "255 total check-ins, 155 unique users." Same issue. Fix: present Gully's-specific stats as the headline. If showing combined numbers, label them clearly as "Endicott campus pilot — two venues."

Always note that these are pilot signals, not proven causal lift.

---

## Tone

Clear, confident, modern, minimal, culturally aware, premium. No buzzwords. No consulting-speak. No startup fluff. No nightlife bro-energy. No loyalty app language.

**Patterns to follow:**
- Short sentences that land hard
- Fragments OK when punchy
- Never "comprehensive," "robust," "leverage," "unlock," "empower," "revolutionize"
- Never "check-in app," "reward system," "earn points," "gamification"
- Prefer: "show up," "regular," "remember," "presence," "session," "return"

**The movie trailer principle:** The website should feel like a movie trailer, not the screenplay. Intriguing, not over-explaining.

---

## What to Keep Private

Never mention or reveal:
- Exact scoring or graph mechanics
- Internal data model details
- Growth playbook or expansion sequencing
- Competitive moat specifics
- Specific retention cohort breakdowns beyond what's already public
- Future roadmap past "semester recaps" and "semester-end identity record"
- Any proprietary backend strategy
- Specific AI capabilities (the site should not mention AI at this stage)

---

## Privacy — Address It Explicitly

Investors and students both have privacy concerns. The current students page has a privacy note — keep it and strengthen it if needed.

Privacy frame: Sway is a privacy-conscious participation platform. Students own their participation history. Venues see behavioral patterns (who came back, which events created regulars), not individual identities. Sway does not sell student data, does not share check-in history publicly by default, and does not track location passively.

---

## Page-by-Page Instructions

### Homepage (`app/page.tsx`)

**Hero section:**
The current hero cycles through: "fun. remembered. social. yours." with typewriter animation. The animation mechanic can stay — just update the word list and surrounding copy.

Word list (replace current): `remembered.` / `counted.` / `yours.`

Hero static headline (the part that doesn't cycle): 
- Option A: `Going out should be` [cycling word]
- Option B: `Your real life should be` [cycling word]
- Current text uses: "Make your nights" — update to match Option A or B above

Subheadline (below hero words):
Replace current subheadline with:
> Sway is the check-in layer for real-world social life. Tap in at the places you actually go. Build your record. Become a regular.

CTA buttons: 
- Primary: `Join early access`
- Secondary: `Request a pilot`

**"How it works" or student-facing feature section (if exists):**
Lead with student emotion before venue analytics. The check-in is the input. Memory, regular status, and semester recaps are the output.

**Venue teaser (if exists):**
Keep practical. "Know who comes back." "No POS replacement." "No staff workflow change."

**Social proof / pilot stats (if exists):**
Use Gully's-specific numbers (69 users, 37.7% return). Label clearly as Spring 2026 pilot.

**Any "What is Sway" section:**
Replace abstract or technical copy with:
> Sway turns going out into memory, status, and identity — starting with campus communities. Students build a real-life timeline. Venues learn what brings people back.

---

### Students Page (`app/students/page.tsx`)

This page is largely well-written. The "I went somewhere. That should count." closing CTA is strong — keep it.

**Hero:**
Current: "Your nights should not disappear."
This is good. Keep it. Subheadline is also good.

**What needs updating:**
- The `PhoneSection` section label says "Your Sway Card" — good, keep it. Strengthen the body copy:
  > Sway Card is your real-life record. Tap in at bars, gyms, events, campus spots. Your Card shows everywhere you've actually shown up — not what you posted, not what you said you'd do. What you actually did.
  
- Bullet list items (currently: "Visits tracked at each venue," "Regular status earned by showing up," etc.) — these are good. Consider adding: `"Semester recap — see your whole campus story at the end of the year."`

- `Features` section headline currently: "Real life should be as remembered as your Spotify history." — This is excellent. Keep it.

- Feature cards — current copy is solid. Update the Privacy card body:
  > Your check-in history is yours. Sway does not sell your data, share your history publicly, or track you when you're not checked in. Venues see patterns — not you specifically.

- `PrivacyNote` section — current copy is good. Keep. Consider making the opening line more direct:
  > Sway does not sell your data. Full stop.

---

### Venues Page (`app/venues/page.tsx`)

**Hero:**
Current headline: "Know who actually comes back."
This is strong. Keep it.

Current subheadline: "Sales tell you what happened. Sway tells you who came back. Run beside your existing operations — no POS replacement, no payment changes, no staff workflow change."
This is good. Keep it exactly.

**Problem section:**
Current headline: "POS shows transactions. Not repeat presence."
Strong. Keep it.

The two-column comparison (what POS tells you vs. what it can't) is effective. Keep the structure. Update the "what POS cannot tell you" column to include:
- Who came back last week
- Which regulars you're at risk of losing
- Which events create repeat visits
- Which nights build habits vs. one-time traffic
- Whether students are becoming regulars or one-and-dones

**WhatVenuesSee section:**
The six cards are good. Update "Returning students tonight" to:
- Title: "Tonight's familiar faces"
- Body: "Real-time view of how many students who have been here before are checking in right now."

**HowItWorks section:**
Current copy is clean. Minor update to Step 3 body:
> See who came back, which events created regulars, which nights build repeat behavior — without asking staff to change anything.

**NoFriction section:**
Headline: "Sway runs beside your venue. Not inside it." — Strong. Keep.
The three cards are accurate and clear. Keep them.

**VenueProof section (MUST FIX):**
Current shows: "255 total check-ins, 155 unique students, 81% activation rate, 37% return signal"

Replace the four stat cards with:
- `69` — Gully's students
- `37.7%` — return signal
- `9 wks` — deployment
- `0` — incentives

Update the disclaimer paragraph below the stats to:
> Pilot ran 9 weeks at Gully's — a bar adjacent to Endicott College in Beverly, MA. Zero paid marketing, zero incentives, zero staff workflow changes. 37.7% of students who checked in came back and checked in again. These are pilot signals, not proven causal lift. Fall 2026 deployment is next.

---

### About Page (`app/about/page.tsx`)

**Hero:**
Current: "The internet remembers everything except real life."
Strong opener. Keep it.

Current subheadline: "Sway exists because real-world participation should not disappear..."
Update to be more direct and emotionally resonant:
> Sway exists because real-world participation should not disappear. You go to the same bar every Thursday. You show up to every team night. You're there for the moments that actually matter. Sway remembers all of it.

**WhatSwayIs section:**
Current headline: "Participation memory and repeat-behavior infrastructure."
Slightly technical. Update to:
> The check-in layer for real life. Starting with campus.

The four cards (for students / for venues / the check-in / the graph) are solid. Update "The graph" card body:
> Multiple venues, events, and sessions across a campus become a participation record — the first real picture of how a student actually moved through their college years. That record is yours.

**WhatSwayIsNot section:**
Headline: "Clear positioning matters." — Fine, but consider:
> Sway is not a loyalty app, a payments tool, or a POS replacement. Here's what it's not.

The six "Not X" cards are accurate and well-written. Keep them.

**WhyCampusFirst section:**
Current headline: "Dense, repeated, identity-forming participation." — Strong. Keep.
Current body paragraphs are good. Keep them.

**Vision section:**
Current headline: "The participation graph." — Keep.
Current pullquote: "Single-node participation creates a receipt. Multi-node participation creates identity." — This is excellent. Keep exactly as-is.

Update the body paragraph above the pullquote:
> Sway's long-term direction is a campus participation record — not curated highlights, not a social feed, not what you posted. The actual places you kept showing up. Four years of real-world identity, remembered.

CTAs at bottom: "View the pilot" and "Get in touch" — appropriate. Keep.

---

### Pilot Page (`app/pilot/page.tsx`)

**Hero:**
Current headline: "Live at Gully's. Built for campus density." — Good. Keep.
Update subheadline to add the "no incentives" emphasis higher:
> Sway ran a 9-week pilot at Gully's — a bar adjacent to Endicott College in Beverly, MA. Zero paid marketing. Zero incentives. Zero staff workflow changes. What follows are pilot signals, not proven causal lift.

**Stats section (MUST FIX):**
Current top banner shows combined numbers (255 check-ins, 155 unique users). These are outdated and blend venues.

Replace the top stats banner with a two-tier layout:

Tier 1 — Gully's (lead with this):
- `69` — Gully's students
- `37.7%` — return rate (2+ visits)  
- `23%` — reached 3+ visits
- `9 wks` — deployment
- `0` — incentives

Remove or demote the "155 unique users / 255 check-ins / 81% activation" combined numbers. If you keep them, label clearly as "Endicott campus pilot (two venues combined)" and put them in a secondary section.

**WhatWeTested section:**
Current copy is honest and strong. Keep it.

**WhatWeLearned section:**
Headline: "Signals from 9 weeks of real-world participation." — Keep.
The four learning cards are solid. Update the return signal card:
- Current: "37% of Gully's users showed a return signal."
- Update: "37.7% of Gully's students came back." Remove the hedging sentence at the end and replace with: "Gully's-only data. The gym ran a separate experiment with different return dynamics."

---

## CTAs — Use These Exactly

**For students:** `Join early access` (links to `/students/early-access`)
**For venues:** `Request a pilot` or `Request a venue pilot` (links to `/venues/request-pilot`)
**For campus partners:** `Bring Sway to your campus` (can link to `/contact`)
**Neutral:** `View pilot results` (links to `/pilot`)

---

## What Not to Do

- Do not add sections, pages, or navigation items
- Do not change fonts, colors, spacing, or layout
- Do not add animations or new interactive elements
- Do not mention specific future features (AI, NFC hardware, Apple Wallet) as live products
- Do not claim the pilot proved causality — "signal" and "pilot" language only
- Do not use "loyalty," "rewards," "earn points," "gamification," "streak" (unless it's already in a feature card with the right framing)
- Do not add emojis unless they already exist in the component
- Do not remove the privacy note on the students page
- Do not change copy length significantly — if a headline is 6 words, keep it around 6 words

---

## After You're Done

Run through this checklist:

- [ ] Hero headline updated and clearly communicates what Sway is
- [ ] Student-facing copy leads with memory/identity, not analytics
- [ ] Venue-facing copy is practical and ROI-clear without overpromising
- [ ] Privacy language is explicit and reassuring on students page
- [ ] Pilot numbers are Gully's-specific (69 users, 37.7% return) where leading
- [ ] No fabricated or blended numbers presented without labels
- [ ] No payments, crypto, AI, or loyalty framing anywhere
- [ ] All CTAs use the approved language above
- [ ] "pilot signal, not proven causal lift" disclaimer appears wherever stats are shown

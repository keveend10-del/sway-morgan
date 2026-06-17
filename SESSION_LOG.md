# Sway — Morgan Session Log

## Purpose
Running log of every work session. Updated each session so we always know where we left off.

---

## Session 001 — 2026-06-08

### Context at Session Start
- Opened with stale context (pilot treated as live). Corrected immediately.
- Updated FOUNDER_CONTEXT.md with June 2026 PDF.
- Pilot is COMPLETE. Summer = analysis + prep phase.

---

### Gully's Pilot Results (confirmed)
- 255 total check-ins
- 81% activation rate
- **26% blended return rate** (Gully's alone = 37%, gym dragged it down)
- 9 weeks, zero incentives, zero marketing, no staff workflow changes
- Two venues ran: Gully's and Endicott Gym

---

### Frequency Distribution Data (excl. test accounts)
| Cohort | All Venues | Gully's | Endicott Gym |
|---|---|---|---|
| Unique users | 155 | 67 | 92 |
| 1 visit only | 119 (76.8%) | 42 | 81 |
| 2+ visits | 36 (23.2%) | 25 (37%) | 11 (12%) |
| 3+ visits | 23 (14.8%) | 16 | 7 |
| 5+ visits | 12 (7.7%) | 8 | 4 |
| Avg days between (returners) | 11.4 | 15.8 | 2.5 |

**Note:** Keveen Delgado and Jack Koutrobis appear in the loyal_returners_3plus.csv file.
Confirm whether they are included or excluded from the 155 count.

---

### Key Data Files
- `data/loyal_returners_3plus.csv` — 23 users with 3+ visits
- `data/one_and_done.csv` — 119 users with exactly 1 visit

---

### Analysis Findings

**The Feb 3 founding cohort is the real signal.**
Students present at Gully's opening discovered Sway organically. That cohort produced:
- Bennett Fici: 22 visits, 3.71-day avg cadence (all Gully's)
- Konrad Krysztoforski: 13 visits, 5.84-day avg (all Gully's)
- Multiple 8-visit users from the same night

**April 23 one-and-dones are not real churn.**
Hard launch event at Gully's — 14 people scanned in 2 hours. Semester ended 2 weeks later.
Signup via venue QR = auto-logged first visit (by design). These users didn't churn — they ran out of runway.

**Gym launch wave is the same pattern.**
March 27–31 gym launch produced 60+ one-time signups. Event-driven, not organic. Most never returned.

**Cross-venue transfer = near zero.**
Only 2 real cross-venue users in 3+ cohort (Jason Ferrandino, Anna McDonald), excluding founders.
Identity portability thesis unproven — expected at this stage.

**Brian Carew anomaly.**
8 visits in 21 days (Feb 3–24), then stopped. Unknown why. Worth investigating.

---

### Strategic Decisions Made

1. **Lead with Gully's 37%, not blended 26%** when pitching.
2. **Event-driven launch pushes don't convert to habit.** Organic discovery (Feb 3 cohort) outperforms prompted signups. Don't do another April 23-style launch event.
3. **Entrance hallway tap station = right product direction for Fall.**
   - 6x5ft hallway between outer and inner door at Gully's = forced chokepoint
   - Single NFC tap station mounted there > scattered QR codes around bar tables
   - Solves discovery problem and staff dependency simultaneously
4. **Staff ask for Fall = one sentence at the door.**
   - "Scan here, it's our online Gully's." That's the entire ask.
   - Door person says it, not bartenders.
5. **ID verification pitch = separate two things:**
   - Student identity verification (Sway can do this — enrolled student confirmation) ✅
   - Age verification for alcohol service (legal liability risk, don't own this) ❌
   - Safe pitch: "Sway confirms they're an Endicott student. You still check ID for age."
6. **School database partnership = Phase 3, not Fall 2026.**
   FERPA, data agreements, admin sign-off = institutional sales timeline, not summer.

---

### Interview Priority List
1. **Bennett Fici** (bfici@mail.endicott.edu, 617-610-9309) — 22 visits, all Gully's. Key question: did Sway give him a reason to return, or does he just go to Gully's constantly?
2. **Konrad Krysztoforski** (kkrysztoforski@mail.endicott.edu) — 13 visits, weekly cadence.
3. **Brian Carew** (bcarew@mail.endicott.edu) — 8 visits in 21 days then stopped. What happened?
4. **Hannah Lord or Tierney Kelley** — Feb 3 one-and-dones. Had months to return. Didn't. Why?
5. **Jason Ferrandino** — only real cross-venue user. Did he notice? Did Sway feel different at each venue?

---

### Open Questions
- Are Keveen + Jack in the 155-user count? If yes, real unique user count = 153.
- What does Bennett say when asked why he kept coming back?
- Has Gully's confirmed Fall redeployment? Willingness-to-pay conversation not yet had.
- What is the exact physical layout of the Gully's entrance hallway for tap station placement?

---

### Where We Left Off
- Data analysis complete for Session 001
- CSV files saved to `data/` folder
- Interview framework identified, no interviews scheduled yet
- Gully's Fall conversation not yet had
- Next: schedule Bennett Fici interview + Gully's manager call

---

_Next session: Update with interview results, Gully's Fall conversation outcome, any product decisions._

---

## Session 002 — 2026-06-08 (same day, deck review)

### Context at Session Start
- Deck audit requested before sending to Gilda Doria (semester-long internship supervisor and mentor).
- Goal: strategic feedback, potential intros, credibility — not fundraising.
- Deck had multiple fabricated stats and wrong framing. Full audit run against confirmed pilot data.

---

### What We Did

**Full slide-by-slide audit → output saved to `DECK_AUDIT_GILDA.md`**

Major findings:

1. **Slide 6 (critical)** — Two fabricated stats identified:
   - "60% of active Gully's regulars checked in during first month" — undefined denominator, not in data
   - "25% increase in repeat check-ins after recognition rollout" — **recognition rollout never happened. Stat doesn't exist.**
   - Replacement headline: "37% of Gully's users returned — with no incentives, no recognition features, and no payments."

2. **Slide 12 (critical)** — $100K SAFE at $3M cap is investor language. Sending to a non-investor mentor signals confused relationship framing.
   - Replaced entirely with: what we're working on + where feedback would help most.

3. **Slide 13 (critical)** — "Founding engineer (conversations active)" is false. No conversations active.
   - Replaced with accurate team framing: solo founder-led pilot, exploring technical collaborator.

4. **Slide 9** — Fabricated LTV/CAC metrics ($3,600 LTV, $400 CAC, 9:1 ratio). No venue has paid. No sales CAC incurred.
   - Labeled everything as modeled/unvalidated. Payments layer demoted from coequal Phase 2.

5. **Slide 11** — Spring 2026 listed as future. We're past it.
   - Marked complete with real data. Fall 2026 reframed as "in planning, pending venue confirmation."

6. **Slides 1, 2, 4, 5, 7, 10** — Various overclaims and payments-forward framing.
   - "Live at Gully's" → "Piloted at Gully's Spring 2026."
   - Cut "Identity-Powered Commerce" tagline. Replaced with "Identity-Powered Venues."

---

### Confirmed Data Used in Audit

| Metric | Gully's | Endicott Gym | Combined |
|---|---|---|---|
| Users | 67 | 92 | 155 |
| Return rate (2+ visits) | 37% | 12% | 23.2% |
| 3+ visits | 24% | — | 14.8% |
| 5+ visits | 12% | — | 7.7% |
| Avg return cadence | 15.8 days | 2.5 days | — |
| Incentives / staff changes / payments | None | None | None |

---

### Priority Order for Deck Fixes (before sending)

| Priority | Slide | Issue |
|---|---|---|
| 1 | Slide 6 | Rebuild with real data. Remove fabricated stats entirely. |
| 2 | Slide 12 | Replace SAFE terms with mentor-facing content. |
| 3 | Slide 13 | Remove false founding engineer claim. |
| 4 | Slide 9 | Label LTV/CAC as modeled. Demote payments. |
| 5 | Slide 11 | Mark Spring 2026 complete. Fix Fall framing. |
| 6 | Slide 1 | Fix cover language. |
| 7 | Slide 5 | Cut payments tagline. |
| 8 | Slides 2, 4, 7, 10 | Minor copy fixes. |

---

### Where We Left Off
- Deck audit complete. `DECK_AUDIT_GILDA.md` is the source of truth for edits.
- Deck has NOT been edited yet — edits are queued, not applied.
- Three slides will damage credibility if sent as-is: **6, 12, 13.**

---

### Next Session Starting Points
1. **Apply deck edits** in order of priority (Slides 6 → 12 → 13 first).
2. **Schedule Bennett Fici interview** — still pending from Session 001.
3. **Have Gully's Fall redeployment conversation** — willingness-to-pay + NFC tap station discussion.
4. Confirm whether Keveen + Jack are in the 155-user count.

_Do not send deck to Gilda until Slides 6, 12, and 13 are fixed._

---

## Session 003 — 2026-06-10

### Context at Session Start
- No session logged on June 9. Last work = June 8 (pilot analysis + deck audit).
- Kev brought full notes from meeting with Gina Deschamps (Engel Center Chair, Endicott).

---

### Gina Deschamps Meeting — Key Outcomes

**Delko / Angle Center:**
- Social media contract ~$500/month — "consider it a yes" pending budget confirmation from Brian Delgado (finance).
- Onboard Keveen as vendor under "Delco" (Delgado & Couture). 1099 form needed.

**EIR Opportunity:**
- Gina exploring full-time EIR role for Kev (5 days/week, ~$35k range implied).
- She can access ~$10k from existing budget. Exploring more via Taylor.
- Plans to propose a dedicated EIR fundraising fund.
- Framing: Sway as a live startup ecosystem on campus with student interns.
- Keep EIR role and GA roles separate.
- IP/investment in Sway: Gina interested but needs legal structure first. David (Foundry) = potential lawyer resource.

**Sway — Fall 2026:**
- NFC tap-to-scan working (confirms hallway station direction from Session 001).
- App Store submission target: end of next week (~June 17).
- LOI/letter of intent needed from Gully's for investors.
- Meet with Melissa (Sodexo) to formalize Gully's + gym as first Fall locations.

**Delco agency:**
- Website + client portal built.
- Gina offered intro: Journeyman Press (commercial printing, New Bedford) — free audit as entry point.

**Harvard/Foundry Bootcamp:**
- 2 weeks left (ends late June).
- Final deliverable: video pitch + deck → auto-applies to Catalyst program.
- Catalyst: top 30 founders compete for $100k non-dilutive (1 winner).

---

### Where We Left Off
- Gina meeting notes recorded. No new strategic decisions made yet.
- To-do list below is the operating surface for next session.

---

_Next session: Work through to-do list. Priority: App Store + YC app + deck fixes + EIR job description._

---

## Session 004 — 2026-06-10 (Sway 2.0 + Pressure Test review)

### Context at Session Start
- Kev shared two documents: Sway 2.0 Participation Graph Thesis + Sway Strategic Pressure Test (June 2026).
- Requested co-founder read + agent team weigh-in.

---

### Documents Reviewed

**Sway 2.0 Participation Graph Thesis**
- Vision expansion: identity infrastructure → participation layer for all real-world communities
- "You show up. Sway remembers." — strongest tagline produced so far.
- New features: Circles (participation groups, not chat groups), Wrapped (Spotify Wrapped for real life)
- Revenue phases: Venue SaaS → Community SaaS → Sponsorship → Premium Identity → Payments

**Strategic Pressure Test (advisor-compiled, June 2026)**
- 5 key vulnerabilities: identity thesis may not be paid problem, 37% return rate uncontrolled, verified presence not actually verified, check-in habit fragile, TAM math dangerously small
- Venue type problem: campus bars are wrong first paying customer (captive, low urgency)
- One-number hook concept: show operator one insight they've never seen in 60 seconds
- Graduation = 25% annual churn by design
- 5 immediate priorities ranked

---

### Agent Findings

**Marcus Webb (Financial Analyst):**
- Community SaaS per campus: ~$1,225/month ceiling. Additive (10–15% lift), not transformative.
- Sponsorship doesn't activate below 50k verified profiles. Phase 3 placement is correct.
- Path to $50k MRR: 150 venues + 250 orgs across 10–15 campuses. 24–30 months.
- Sway 2.0 lifts TAM ceiling from $5–10M to $30–50M ARR — but only if community SaaS and sponsorship both prove out.
- Fall experiment: one venue + one club + one Greek org at Endicott = three account types, one campus.

**Derek Santos (Venue Sales Specialist):**
- One-number hook: "Your top customer visited 22 times. You have no idea who he is. Here's what we captured without changing a single thing about how you operate."
- Anonymity of regulars is the gut-punch, not the percentage.
- Salem = priority second market (Salem State off-campus bar scene = captive-adjacent but competitive).
- Specific targets: Bit Bar Salem, Ledger Restaurant & Bar, Longboards Beverly.
- Cold outreach line: "You ran 8 trivia nights this spring. I can tell you exactly which customers came once and never came back."

**Alex Park (Product Growth Analyst):**
- Strongest causation case: Feb 3 founding cohort (organic, no incentive, highest frequency). Sway = only differentiating variable.
- 15.8-day discretionary return cadence at Gully's vs. 2.5 days at gym (obligation). Discretionary repeat is the signal.
- Fall causation experiment: split by entry point, use POS counts as denominator for non-Sway control.
- Brian Carew anomaly: top hypothesis = novelty loop broke (early adopter responding to newness, not habit). If true, 5+ visit cohort measures curiosity not stickiness.
- **Interview Carew before Fall. One conversation resolves this.**

---

### Strategic Decisions Made

1. **Sway 2.0 vision is directionally right but premature to operationalize.** File it. Pull it out when 3+ campuses running and need investor story.
2. **Pressure Test is the operating document right now.** Its 5 priorities are the move order.
3. **Brian Carew interview is now highest priority** — above Bennett Fici. Novelty hypothesis must be resolved before Fall.
4. **One-number hook is the Bennett Fici / 22 visits framing.** Get Gully's management on record whether they knew their regulars before Sway.
5. **Salem outreach this week** — Bit Bar first, then Ledger. Non-pitch conversation only.
6. **Gully's LOI** — lock informal intent at $149–$299 before Foundry bootcamp ends (late June).

---

### Move Order (Priority)
1. Interview Brian Carew
2. Shape Bennett Fici hook → get Gully's manager quote
3. Reach out to Bit Bar Salem (non-pitch, 45-min conversation)
4. Get Gully's LOI from Melissa (Sodexo) meeting
5. Design Fall causation experiment (split entry point, use POS as control)
6. Continue: App Store target June 17, deck fixes, EIR job description

---

_Next session: Report on Carew interview outcome. Salem outreach status. Gully's LOI progress._

---

## Session 005 — 2026-06-11

### Completed Today
1. **Brian Carew** — reply received (see interview findings below) ✅
2. **Bennett Fici** — said yes to interview; 5 questions sent via email
3. **Deck** — Kev confirmed slides 6, 12, 13 fixed. Deck sent to Gilda Doria.
4. **Melissa (Sodexo) meeting** — email drafted and sent. Availability offered: June 26 (any time), June 30 (any time), July 1 (8am–2pm). Asked Melissa to include Glenda's email for calendar invite.
5. **Gina Deschamps meeting** — full notes saved to `GINA_MEETING_2026-06-11.md`
6. **EIR job description** — drafted ✅
7. **Brian Cain (President) email** — sent. Vision pitch: Endicott as live startup ecosystem.
8. **Text to David Ferguson** — drafted, asking for pro bono lawyers re: Sway/Endicott IP structure

---

### Brian Carew Interview — Full Findings (PDF received June 12)

**Source:** Written Q&A responses, submitted via PDF

**His exact words (key quotes):**
- "I was going to Gully's the same amount as when I downloaded the app — that didn't change."
- "Visit count crossed my mind only when scanning in but then put the app away and forgot about it for the rest of the night."
- "It was mostly just a thing I did. I felt like a regular because the bartenders knew my order. That's what makes someone feel like a regular — the face to face relationships."
- "No one really stuck with it since there wasn't really a point or goal to reach that was some form of reward for X amount of visits or check-ins."
- "It would not [change anything]. Most people found out Gully's themes and promos through the Instagram page."

**Context clarified:** Gully's mug club "member of the week" = Gully's own program. Kev surfaced it in the Sway app. Brian saw it but it highlighted someone else. Broadcast recognition = zero identity value.

**Conclusions:**
1. **Sway did not change his behavior.** 8 visits in 21 days = he was already a regular before Sway. Sway measured existing behavior, did not create new behavior. Critical data point.
2. **Novelty hypothesis confirmed.** Alex Park called it in Session 004. Case closed.
3. **The real identity signal is venue-side, not student-side.** "Bartenders knew my order" = what made him feel like a regular. Sway's job is to give the venue operator that same recognition at scale — for the regulars no bartender knows yet. This is the pitch.
4. **Student-facing value prop is not legible.** He tried to show friends, nobody stuck. Can't explain the "why." Missing: a moment at first tap that makes the value obvious.
5. **His four suggestions are all thesis drift.** GPS auto-checkin (passive = corrupts signal), Instagram nav (social feed before Gate 1), drink tracking/leaderboards (Untappd + liability), skip-the-line incentives (discount-adjacent loyalty app). Do not build any of them.
6. **Gully's Instagram does the awareness job.** Students follow IG for promos, not Sway. Fine — Sway's value is at the tap, not before it.

**What this changes:**
- Build priority list unchanged.
- Presence summary screen framing: not just "you've been here 8 times" — "You're one of Gully's 8 regulars this week." Individual count needs to feel earned, not just logged.
- Bennett Fici interview now more important: does 22 visits feel meaningful *to him*, or was it also just a thing he did?

**Do NOT build from Carew's suggestions.** He wanted Untappd + a loyalty rewards app + a social feed. That product exists. It didn't win.

---

### App Product Priorities — Locked In This Session

Sequence before June 17 App Store submission. Do not add anything outside this list.

| Priority | What | Why |
|---|---|---|
| 1 | **Presence summary screen** | Carew validated gap directly. At every tap: visit count, last visit, cross-node history. Personal mirror, not public stage. |
| 2 | **Member of the week — demote or remove** | Gully's mug club content. Keep small if at all. Put personal stats above it. Never lead with someone else's win. |
| 3 | **App polish / consistency sweep** | Typography, spacing, button states, loading states. Must be clean before App Store submission. |
| 4 | **NFC tap flow** | Instant confirmation. "Welcome back" ≠ "Welcome." Haptic or fast animation on tap. Frictionless first-time flow. |
| 5 | **Empty state for new users** | What does a student see before their first tap? One-line explainer + where to tap + what happens next. |

**Core principle locked:** Build mirrors, not stages. Individual presence feedback > broadcast recognition.

---

### Angle Center Deliverables — Produced This Session

- **EIR job description** — full modern JD drafted for Gina's funding conversations
- **Email to Brian Cain (President)** — vision pitch sent. "Endicott as live startup ecosystem." No money talk.
- **Text to David Ferguson** — drafted. Asking for pro bono lawyers to review Sway/Endicott IP + partnership agreement.
- **Angle Center programming ideas** — 10 new ideas across programming, institutional positioning, and Sway synergies
- **Meeting notes** — full Gina meeting saved to `GINA_MEETING_2026-06-11.md`

**Key people map:**
- **Brian Cain** = President of Endicott. Vision buy-in. Don't bring money into this conversation.
- **Brian Delgado** = Finance. Budget confirmation for Delco social contract ($500/mo). Happens after Cain is on board.
- **David Ferguson** = Foundry connection. Resource for lawyers on IP structure.
- **Gina Deschamps** = Angle Center Chair. EIR champion. Coordinating Taylor for additional EIR funds.
- **Taylor** = Gina's source for additional EIR funding — name only, no other context yet.

---

### Status
- App polish in progress. App Store submission target: June 17.
- EIR job description drafted, in Gina's hands.
- Brian Cain outreach initiated.
- David Ferguson text drafted — send pending.

### Open
- Bennett Fici reply pending
- Gully's LOI — waiting on Melissa/Glenda reply
- Salem outreach (Bit Bar) — not yet started
- Fall causation experiment design — not yet started
- Brian Cain reply — pending
- David Ferguson response — pending
- Brian Delgado budget confirmation — pending Cain buy-in first

_Next session: Bennett Fici reply. Melissa reply. Brian Cain response. App build progress check against priority list above._

---

## Session 006 — 2026-06-13

### Context at Session Start
- Last session: June 11. Two days of work logged offline.
- Bennett Fici reply received. David Ferguson replied. Melissa still pending.
- App work started. UX direction decision made.

---

### Bennett Fici Interview — Full Findings

**Source:** Written Q&A responses (PDF)

**His exact words (key quotes):**
- "I was going to Gully's the same amount as when I downloaded the app — that didn't change."
- "Visit count crossed my mind only when scanning in but then put the app away and forgot about it for the rest of the night."
- "It was mostly just a thing I did, I felt like a regular because the bartenders knew my order. That's what makes someone feel like a regular — the face to face relationships."
- "A few times but no one really stuck with it since there wasn't really a point or goal to reach that was some form of reward for X amount of visits or check-ins."
- "It would not [change anything]. Most people found out Gully's themes and promos through the Instagram page."

---

### Two-Interview Pattern — Now Confirmed

Fici (22 visits) and Carew (8 visits) gave near-identical answers across all five questions. This is no longer a single data point.

| Question | Carew | Fici |
|---|---|---|
| Did Sway change frequency? | No | No |
| Did visit count mean anything? | Glanced at tap, forgot it | Glanced at tap, forgot it |
| Did it make you feel like a regular? | "Bartenders knew my order" | "Bartenders knew my order" |
| Did anyone stick with it? | No | No |
| Would you notice if it disappeared? | No | No |

**Both used "bartenders knew my order" unprompted.** That is the product insight.

---

### Conclusions

1. **Sway did not change behavior for either top user.** Both were already regulars. Sway measured existing habit, did not create new habit.
2. **Student-facing value prop is not legible.** Two power users — 30 combined visits — felt nothing meaningful from the app. This is a Gate 1 problem, not a UI problem.
3. **Operator thesis strengthened.** "Bartenders knew my order" = the recognition Sway must deliver at scale, for the regulars no bartender notices yet. That's the pitch to Gully's management.
4. **Presence summary screen is necessary but not sufficient.** Seeing "22 visits" produces no feeling if there's no context for why it matters. Fall UX problem: make the count feel earned, not just logged.
5. **Fici's four suggestions = all thesis drift.** GPS auto check-in (corrupts verified presence), Instagram nav (social feed before density), drink tracking/leaderboards (Untappd + liability), skip the line / free merch (discount loyalty app). Do not build any of them.

---

### Updates

- **David Ferguson** — replied. Touch base Monday June 16. Kev's roommate's father. Brought in as Spark Tank judge at Endicott. Legal resource for EIR structure — specifically IP ownership and partnership agreement between Kev/Sway and Endicott. Pro bono ask.
- **Brian Gorman (SCORE mentor)** — assigned June 12. Near Boston. Online meeting. Asked for Kev's availability "next week" (= this week, June 16+). Kev replied June 12 but did NOT include times. Follow-up with availability still needed. He's aware of both Sway and Delko — decide which to lead with before meeting.
- **Melissa (Sodexo)** — no reply yet. Gully's LOI still open.
- **App work** — started. UX direction decision made (see below).

---

### App UX Direction — Locked

Target feel: **Airbnb-level polish.** Consistent system, clean hierarchy, venue pages match app-wide theme.

Specific direction:
- Every screen uses same design language (typography, spacing, color, component states)
- Venue pages elevated to match polish of identity/profile screens — not treated as secondary
- UX should feel like a product with craft, not a prototype
- Airbnb reference: trust-building through consistency, both sides of the experience feel cared for

This complements Session 005 priority list. Presence summary screen + NFC tap flow + polish sweep all point the same direction.

---

### Open

- Melissa/Gully's LOI — still waiting
- David Ferguson call — Monday June 16
- Brian Cain reply — pending
- Salem outreach (Bit Bar) — not started
- App build in progress — App Store target June 17
- Fall causation experiment design — not started

_Next session: David Ferguson call outcome. Melissa reply. App Store submission status. One-number hook for Gully's operator conversation._

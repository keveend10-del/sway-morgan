# Sway — Business Model Execution Plan
*Diamond-Square Framework + Participation Economic Analysis*
*Generated: June 2026*

---

## Executive Summary

Sway is the participation OS for real-world communities. It turns completed physical presence into identity, memory, recognition, and operator signal. The tagline is the thesis: **You show up. Sway remembers.**

The beachhead is campus. The wedge is the campus bar. The proof is Gully's at Endicott College — 255 check-ins, 81% activation, 26% return rate, 9 weeks, zero incentives, zero paid marketing, no staff workflow changes.

**What this document is:** A rigorous pressure test of whether Sway can become a real business, using the Harvard Business School Diamond-Square Framework, a custom Participation Economic Analysis, and a practical 90-day Fall 2026 execution plan.

**What this document is not:** A pitch deck. A fundraising narrative. A business plan that pretends things are proven that aren't.

**The key business hypothesis:** If completion-based recognition increases repeat participation, then operators and communities will pay for visibility, programming insight, and access to the participation graph.

**The current honest state:**
- Behavior signal: real and differentiated (students return without rewards — this almost never happens)
- Revenue: zero (Gully's has not paid)
- Multi-node proof: zero (only one venue has ever been live)
- Willingness-to-pay: unvalidated

**What Fall 2026 must produce** to make Sway investor-ready at pre-seed:
1. Gully's on a paid contract at any price
2. One second node live at Endicott
3. Session depth data showing ≥20% of users hit 3+ sessions
4. One documented operator decision made from Sway data

Everything in this document is built toward that outcome.

**Identity first. Repeat second. Messaging earned. Payments optional.**

---

# Section 1: Diamond-Square Business Model Analysis

---

## 1A. Customer Value Proposition

### For Students

**The core problem Sway solves:** Campus life has no memory. You show up to 40 events, become a Gully's regular, run a 5K at the gym every week — and nothing captures it. No record, no recognition, no one knows. Your campus identity is invisible.

**What Sway delivers:**

**Identity you earn by showing up.**
Not a profile you fill out. Not followers you accumulate. A participation record built entirely from physical presence. A student who's been to Gully's 18 times has a different campus identity than one who's been once — Sway makes that visible and portable.

**Memory that follows you across nodes.**
Right now, your campus history lives nowhere. Sway creates a persistent timeline — every session, every event, every space — across the entire campus ecosystem. By senior year, that's four years of participation history. Nothing else builds this.

**Recognition before you have to ask for it.**
When a bartender or community manager can see you're an established regular, recognition happens naturally. You don't have to perform it. The status is embedded in the infrastructure. This mirrors what Blackbird did for restaurant regulars — but on campus, where the social stakes are higher and the density is tighter.

**Regular status that means something socially.**
On a campus of 1,200 students, being recognized as a genuine community regular carries peer weight. Sway makes that status legible — to the venue, to the community, to the student's own sense of belonging. This is not a badge. It's behavioral history made visible.

**Portability across the campus ecosystem.**
Gym sessions, club events, sports games, Gully's visits — one participation graph, one identity. The student who's active across nodes is building something compound. A single-venue app cannot do this.

*Example: A sophomore athlete attends 22 gym sessions, 6 soccer games, 3 club events, and 11 Gully's nights by November. Without Sway, no one knows this person is a campus anchor. With Sway, that identity is visible to anyone operating a node on campus.*

---

### For Venues, Communities, and Operators

**The core problem Sway solves:** Operators are flying blind. They know sales. They don't know who walked in, who came back, what programming drove return behavior, or which customers are building a habit versus passing through.

No existing tool solves this without POS integration, staff workflow changes, or app downloads at the point of entry. Sway captures real presence data with a QR scan — no friction, no staff changes, no rewards required.

**What Sway delivers:**

**Actual attendance vs. assumed attendance.**
Covers vs. sales tell you how many transactions happened. They don't tell you if it was 80 people once, or 20 people four times. Sway distinguishes visit volume from visitor count.

*Example: Trivia night does $1,800 in covers. Was that 200 students once? Or 60 returning regulars? The answer completely changes whether you run it again and how you market it.*

**Who returned and how often.**
Gully's pilot showed 26% return rate with zero incentives. Sway gives operators the ability to track which programming generates that return behavior vs. which programming creates one-time spikes that don't compound.

**Emerging regulars before staff knows them.**
A student who has visited 4 times in 3 weeks is on a trajectory to become a regular. Currently, the bartender has no way to know this unless they recognize the face. Sway surfaces that signal automatically, enabling proactive recognition that accelerates the habit.

**Community overlap data.**
Which communities cluster together? If soccer players and Gully's regulars overlap at 40%, that's a co-programming signal. A soccer viewing night has a built-in audience. No other tool surfaces this without months of manual survey work.

**What programming actually works.**
Not which events had the most people. Which events converted first-timers into repeats. That's a fundamentally different question — and the answer changes programming strategy entirely.

**Who is one-and-done.**
Knowing who never returned, when they came, and what event they attended gives operators an early signal on which marketing channels or event types attract non-sticky traffic.

**Cross-venue behavior (multi-node operators).**
If Endicott runs the gym, Gully's, and the Foundry under one campus relationship, operators can see: students who use the gym 3+ times/week are 2x more likely to attend evening events. This is the kind of insight that justifies a campus cluster deal.

**What currently solves this:** Nothing. Loyalty apps require sign-up before entry, incentive architecture, and staff behavior changes. Reservation systems only capture bookings. POS only captures transactions. Sway captures presence — which is upstream of all of those.

---

## 1B. Technology & Operations

### Check-In Layer (Present and Planned)

**QR Code — Live Now**
Static QR codes placed at venue entry. Students scan on arrival via phone camera — no app download required in initial flow. This is the current Gully's mechanism. Zero staff involvement, zero workflow change. Limitation: cannot validate that the student stayed (time-in vs. scan-and-leave).

**NFC — Planned (Phase 2)**
Near-field tap via phone or Sway Card. Faster than QR, better for high-volume entry moments (event rush, gym turnstile). Enables tap-and-go for returning regulars. Lower friction than QR at scale.

**GPS/Geofencing — Planned (Phase 3)**
Passive presence detection for outdoor or multi-point venues (sporting events, campus quads, festivals). Does not require active scan. Introduces trust complexity — must be paired with validation layer.

**Wallet Pass / Sway Card (Digital) — Planned**
Apple Wallet / Google Wallet integration. Converts the Sway identity into a persistent artifact the student carries. Enables push notifications tied to campus presence. Reduces friction for returning users.

---

### Presence Session Object

A session is the core data primitive. What gets captured on every completed check-in:

```
session {
  user_id
  node_id (venue / community / event)
  session_type (venue visit / event / workout / game)
  entry_timestamp
  exit_timestamp (if available)
  duration (if tracked)
  event_tag (if tied to programming)
  session_status: [pending → complete → abandoned]
  validation_flags
  campus_cluster_id
}
```

**What the session object enables:**
- Frequency analysis per user per node
- Cross-node behavior mapping
- Event-type attribution (which session types generate repeats)
- Community overlap detection
- Timeline construction for student-facing view

---

### Completion Engine

**Current state (QR-only):** Session is marked complete at scan. No exit signal. Duration unknown.

**Challenge:** A student could scan and immediately leave. This is the trust gap in Phase 1.

**Planned completion logic:**
- Time threshold: session marked "complete" if user remains in venue for minimum duration (geofence confirmation or secondary scan at exit)
- Event-tied completion: if session is linked to a time-bounded event, completion is inferred by event end
- Operator confirmation: operator dashboard can flag anomalous scan patterns

**Why this matters:** The integrity of the participation graph depends on sessions reflecting actual presence. Gaming the system (scan-and-leave) degrades the signal for operators and the meaning of the identity for students.

---

### Sway Card

**What it is:** A physical or digital card representing a student's participation identity within a campus ecosystem. Not a payment card. Not a membership card in the traditional sense.

**What it represents:** Your campus presence history, made portable. Analogous to a passport — not what you're entitled to, but where you've been and how often.

**Current state:** Conceptual. The digital analog is the student's Sway profile/timeline. The physical card would serve as a recognition artifact.

**Planned function:** NFC-enabled tap mechanism, replacing QR for returning users. Also serves as a social artifact — something students carry and identify with.

---

### Student Timeline / Recap

**What the student sees:**
- Chronological session history across all nodes
- Session count by node (Gully's: 18 visits, Gym: 34 sessions, Events: 6)
- Milestone markers (first visit, 10th visit, one-year anniversary)
- Campus activity summary (shareable, social-native)

**What motivates return:**
Completion-based recognition — seeing your own participation history, built accurately, creates a pull toward continuation. This mirrors streak mechanics in fitness apps, but tied to real physical presence rather than digital behavior.

**Current state:** Basic session capture exists. Student-facing timeline is in development. The semester recap (shareable campus history) is planned for Fall 2026.

---

### Operator Dashboard

**What operators see today (Gully's pilot):** Check-in counts, basic frequency data.

**What the full dashboard delivers:**
- Visit frequency distribution: 1x / 2–3x / 4+ visitors in a period
- Return rate by event type: which programming generates repeats, not just volume
- Emerging regulars feed: students trending toward regular status
- Community overlap map: which campus communities co-cluster at this venue
- One-and-done analysis: what % of visitors never returned, by first-visit event type
- Cross-node behavior (campus cluster operators): student activity across all nodes

**Decisions the dashboard enables:**
- "Program more trivia nights because trivia converts one-timers to regulars at 2x the rate of live music"
- "Reach out to the soccer team because 35% of their members are already regulars"
- "Stop promoting to the Greek org that drives single-visit volume with no return"

**Current state:** Basic dashboard exists. The full analytics layer is planned for Fall 2026.

---

### Trust and Validation Layer

**The problem:** Any open QR system can be gamed.

**Current approach:**
- QR codes are node-specific and time-rotated (prevents screenshot sharing across sessions)
- Anomaly detection: multiple scans from same device in short window flagged
- Operator-visible flagging: suspicious patterns surfaced in dashboard, not auto-blocked

**Planned additions:**
- Exit scan or dwell-time requirement for session completion
- Device fingerprinting to prevent one device scanning for multiple users
- Venue staff spot-check integration

**Philosophy:** Sway is not building a surveillance system. The goal is signal integrity — enough validation that the participation graph is trustworthy without requiring invasive verification.

---

### Campus Node Admin Tools

**What a campus org needs to run its own node:**
- Node setup: QR generation, event creation, session type configuration
- Event tagging: link sessions to specific events so data is attributable
- Basic analytics: who came, how often, what events drove traffic
- Member roster overlay (optional): match participation data against club membership lists
- Node admin access controls: separate from venue operator access

**Current state:** Not built. Gully's is operated by Sway directly. Multi-node campus admin tools are a Fall 2026 development priority required before the Endicott cluster can scale.

---

## 1C. Market & Commercial Pathway

### Step 1: Single Venue — Gully's (Proven, Paused for Summer)

**Hypothesis:** Students will scan without incentives, and some will return without rewards.

**What was proven:**
- 255 check-ins, 81% activation rate, 26% return rate
- Zero incentives, zero paid marketing, no staff workflow changes
- Presence capture works at the venue level

**What is NOT yet proven:**
- Whether recognition (student seeing their own history) increases return rate
- Whether the operator will pay for this data
- Whether cross-venue participation compounds behavior

**Go signal for Step 2:** Gully's restarts in Fall 2026 with the timeline/recap feature live. If return rate increases from 26% with recognition feature active, the core hypothesis holds.

**No-go signal:** Return rate stays flat after recognition features are live — indicates the product is a novelty, not a behavior driver.

---

### Step 2: Campus Ecosystem — Endicott (Fall 2026 Target)

**Target nodes:** Gully's, campus gym, Foundry/Angle Center, Entrepreneurship Club events, one sporting event series.

**Hypothesis:** Students who participate across multiple nodes develop a stronger campus identity, and cross-node data gives operators more valuable signal than single-node data.

**What must be true before this step:**
- Node admin tools built and functional
- Student timeline live and showing cross-node activity
- At least one non-Gully's node willing to run a QR station

**Metric that proves it:**
- Cross-node participation: % of students active on 2+ nodes within 30 days
- Operator interest: at least one campus org asks for their node's data without being prompted
- Return rate uplift: Gully's return rate meaningfully higher than 26% with recognition active

**Go/no-go signal:** If 30%+ of active students are participating across 2+ nodes by November 2026, the campus ecosystem hypothesis holds and commercial packaging becomes viable.

---

### Step 3: Package the Cluster (Q1 2027)

**What it looks like commercially:**
- One campus-level agreement covering all nodes under Endicott
- Pricing: $149–$299/node/month, packaged as a campus cluster at a slight discount (e.g., 5 nodes at $199/month = $995/month)
- Single point of contact: Dean of Students, Director of Campus Life, or equivalent
- Value proposition to institution: participation data across the campus ecosystem, not just one venue

**What must be true before packaging:**
- Demonstrated cross-node behavior data exists and is legible in the dashboard
- At least one campus decision-maker has seen the cross-node overlap report and found it useful
- Node admin tools are stable enough that campus orgs can self-manage

**Metric:** Signed campus cluster contract, even if discounted for the pilot relationship.

---

### Step 4: Second Campus Replication (Q2–Q3 2027)

**What unlocks this:**
- Endicott cluster is generating clean signal (cross-node data, operator utility, student engagement)
- A repeatable campus sales motion exists (who to call, what to demo, what to promise)
- At least one case study: quantified return rate improvement tied to Sway

**Hypothesis:** The campus playbook is repeatable at student-dense residential campuses with 1,000–5,000 enrollment. The anchor node is always a social venue (bar, student union) where habitual behavior already exists.

**Target campus profile:** 1,200–4,000 students, residential, has an on-campus bar or student union, active Greek life or sports culture, progressive campus life leadership.

**Go/no-go signal:** Second campus closes within 60 days of outreach using the Endicott case study. If sales cycle is longer than 90 days, the pitch or proof point needs rework.

---

### Step 5: Off-Campus Student-Heavy Venues (Q3 2027+)

**When this happens:** After cross-venue portability is proven within a campus ecosystem and at least two campuses are live.

**Why this is Step 5 and not Step 2:** Off-campus venues don't benefit from the campus identity layer until the campus network has density. A bar near a campus gains value from Sway only if the student participation graph is already meaningful.

**Hypothesis:** Students carry their campus participation identity off-campus, and off-campus venues can see which campus communities frequent them.

**Metric:** Off-campus venue retention after 3 months. If the venue isn't seeing meaningful repeat-visitor data tied to campus communities, the off-campus value prop is premature.

---

### Step 6: Dense Real-World Communities Beyond Campus (2028+)

**What this looks like:** Sway's campus playbook applied to other community-dense contexts — professional sports venues, neighborhood bars with regulars, co-working spaces, fitness communities, arts spaces.

**The unlock:** This step is viable only when Sway has proven that the participation graph is portable, that operators pay for the signal, and that students carry their identity across contexts without friction.

**This is infrastructure play territory.** At this stage, Sway is not selling software to venues — it is licensing participation graph infrastructure to community operators across verticals.

**What makes this defensible:** By the time Sway is in 50 campuses with 200+ nodes, the participation graph has a network effect. A student who graduates and moves to a city where Sway is live takes their identity with them. That portability is what creates the moat — not the QR code.

---

## 1D. Economic Viability

### Phase 1: SaaS Per Node ($149–$299/month)

**How Sway makes money now:** Per-node monthly SaaS. A node is any venue, community, or event series running a Sway QR station.

**Pricing rationale:**
- $149/month: basic node, single-venue operator, event series, campus club
- $199/month: venue operator with basic analytics dashboard
- $299/month: venue or campus org with full dashboard, return rate reports, community overlap data

**What must be proven before a venue pays:**
1. Presence capture is reliable and frictionless (no staff workflow changes required)
2. Dashboard shows data the operator finds useful, not just vanity metrics
3. At least one insight from the dashboard has changed an operator decision
4. The operator can articulate what they'd lose if Sway went away

Currently, Gully's is not paying. The pilot was free. That changes in Fall 2026 — or the business model doesn't work.

---

### 12-Month Revenue Model: Endicott Alone

**Scenario A: 3 Nodes**

| Period | Nodes | Avg Price | MRR | 12-mo ARR |
|---|---|---|---|---|
| Oct–Dec 2026 | 3 | $199 | $597 | — |
| Jan–Jun 2027 | 3 | $199 | $597 | — |
| **Total** | — | — | — | **~$7,200** |

**Scenario B: 5 Nodes**

| Period | Nodes | Avg Price | MRR | 12-mo ARR |
|---|---|---|---|---|
| Oct–Dec 2026 | 3 | $199 | $597 | — |
| Jan–Jun 2027 | 5 | $199 | $995 | — |
| **Total** | — | — | — | **~$10,800** |

**Scenario C: 7 Nodes (Campus Cluster Package)**

| Period | Nodes | Avg Price | MRR | 12-mo ARR |
|---|---|---|---|---|
| Oct–Dec 2026 | 3 | $199 | $597 | — |
| Jan–Jun 2027 | 7 | $185 (cluster discount) | $1,295 | — |
| **Total** | — | — | — | **~$13,500** |

**Honest assessment:** Endicott alone does not build a company. It builds a proof of concept with a revenue signal. The value of Endicott in year one is not the $7,000–$14,000 — it is the case study, the cross-node data, and the repeatable playbook.

---

### Unit Economics: Cost Per Node vs. Revenue Per Node

**Revenue per node (steady state):** $199/month = $2,388/year

**Cost to serve one node at steady state:**
- Infrastructure (hosting, data): ~$15–25/month per node
- Support burden: ~$20–30/month blended
- Customer success (time allocation): ~$30–50/month at early stage, declining with scale
- **Gross margin per node: ~75–80% at steady state**

**Cost to acquire one node (CAC):**
- Campus cluster sale (5 nodes): founder-led, 10–15 hours of effort
- Blended CAC at early stage: ~$200–400 per node (time-cost only, no paid acquisition)
- At scale with a sales hire: CAC rises to $600–1,000 per node but payback period still under 6 months

**Payback period:** $199/mo node pays back in ~5 months. Healthy for SaaS.

---

### Cluster ACV Model

| Cluster Size | Avg Price/Node | Monthly | ACV |
|---|---|---|---|
| 5 nodes | $199 | $995 | $11,940 |
| 7 nodes | $185 | $1,295 | $15,540 |
| 10 nodes | $175 | $1,750 | $21,000 |

A 10-node campus at $175/node/month = $21,000 ACV. One campus, one relationship. This is the commercial thesis: campus clusters, not individual venues.

---

### Expansion Math

**10 Campuses (Target: End of 2027)**
- Avg nodes per campus: 6
- Avg cluster ACV: $14,000
- Total ARR: ~$140,000 / MRR: ~$11,700
- *This is venture-fundable signal. Not venture-scale revenue — proof that the playbook replicates.*

**50 Campuses (Target: 2028–2029)**
- Avg nodes per campus: 7
- Avg cluster ACV: $16,000
- Total ARR: ~$800,000 / MRR: ~$66,000
- *Approaching $1M ARR at 50 campuses with a lean team is viable. This is the SaaS ceiling without the infrastructure play.*

---

### SaaS Business vs. Infrastructure Business

**SaaS ceiling:** Sway sells software to operators. Revenue scales with nodes. Business tops out in the tens of millions ARR without a platform shift.

**Infrastructure play:** At 50+ campuses with 500,000+ students in the system, the graph itself has value independent of any single node:
- **Data licensing:** Brands pay for aggregate participation signal (not individual PII). First-party behavioral data brands currently cannot buy.
- **Network effects:** A graduating student takes their participation identity to any city where Sway is live.
- **API/infrastructure licensing:** Event companies, campus software platforms license Sway session infrastructure.
- **Session-gated access (Phase 4):** Once identity is established, session history becomes a credential. Payments become natural rather than forced.

**Honest timeline:** Sway does not have an infrastructure business until it has 10,000+ active students across 10+ campuses. That is 2028 at the earliest. The SaaS business pays the bills while the graph accumulates density.

---

### What Is Proven vs. Modeled

| Claim | Status |
|---|---|
| Students scan without incentives | **PROVEN** (81% activation) |
| Students return without rewards | **PROVEN** (26% return rate, 9 weeks) |
| No staff workflow change required | **PROVEN** |
| Zero paid marketing needed for initial adoption | **PROVEN** |
| Recognition features increase return rate | **UNPROVEN** — Fall 2026 test |
| Cross-node behavior compounds engagement | **UNPROVEN** — requires 3+ nodes |
| Operators will pay $149–$299/month | **UNPROVEN** — Gully's has not paid |
| Campus cluster sales motion works | **UNPROVEN** — no cluster sold |
| Playbook replicates to second campus | **UNPROVEN** |
| Participation graph has licensing value | **MODELED** — not a near-term revenue source |
| $140K ARR at 10 campuses | **MODELED** |

---

# Section 2: Participation Economic Analysis

*An adapted TEA model for participation economics — not traditional tech startup TAM analysis.*

---

## 2A. Key Variables & Definitions

| Variable | What It Measures | Why It Matters | How to Calculate |
|---|---|---|---|
| **Activation Rate** | % of people who encounter Sway and complete a first session | Measures friction at entry | Users completing first session ÷ users who scanned or opened app |
| **Completion Rate** | % of initiated sessions that resolve to complete | Catches drop-off mid-session | Completed sessions ÷ started sessions |
| **7/14/30-Day Return Rate** | % of activated users who return within each window | The core behavioral signal | Users returning within N days ÷ total activated users in cohort |
| **Multi-Node Participation Rate** | % of active users engaging at 2+ distinct nodes | The compounding thesis lives or dies here | Users active at 2+ nodes ÷ total active users in period |
| **Node Density** | Active unique users per node per week | Whether a node is alive — thin density = weak signal | Unique weekly check-ins ÷ node count ÷ weeks |
| **Cluster ACV** | Annual contract value per campus cluster | Revenue modeling unit for institutional sales | Monthly recurring revenue per campus cluster × 12 |
| **Operator Decision Value** | # of documented operator decisions made from Sway data per month | Proves the dashboard is a tool, not a trophy | Count of real decisions traceable to Sway data |
| **Recognition Lift** | Return rate delta between users who received recognition vs. those who didn't | Tests whether identity acknowledgment drives behavior | Return rate (recognized cohort) − Return rate (unrecognized cohort) |
| **Cost per Node** | Fully-loaded cost to onboard and activate one new node | Whether this scales or stays expensive | Total onboarding cost (time + hardware + ops) per node |
| **Revenue per Node** | Average monthly recurring revenue per active node | Monetization density metric | Total MRR ÷ active node count |
| **Participation Compounding Score** | Composite health signal across the participation graph | Single number — is the network strengthening? | Multi-node rate × return rate × completion rate |

---

## 2B. Core Formulas

```
Activation Rate = Users completing first session ÷ Users who scanned or opened app

Completion Rate = Completed sessions ÷ Started sessions

7-Day Return Rate = Users who return within 7 days ÷ Total activated users

14-Day Return Rate = Users who return within 14 days ÷ Total activated users

30-Day Return Rate = Users who return within 30 days ÷ Total activated users

Multi-Node Participation Rate = Users active at 2+ nodes ÷ Total active users in period

Node Density = Unique weekly active users ÷ Active node count

Cluster ACV = Monthly recurring revenue per campus cluster × 12

Operator Decision Value = Count of operator decisions per month traceable to Sway data

Recognition Lift = Return rate (recognized cohort) − Return rate (unrecognized cohort)

Cost per Node = Total onboarding cost (labor + hardware + setup time) ÷ Nodes added

Revenue per Node = Total MRR ÷ Active node count

Participation Compounding Score = Multi-node rate × 30-day return rate × completion rate
```

**Participation Compounding Score interpretation:**
- Score below 0.05 = flat network, no compounding evidence
- Score 0.05–0.15 = early signal, requires more nodes
- Score above 0.15 = compounding behavior emerging, fundable thesis

---

## 2C. Baseline from Gully's Pilot

**Spring 2026 raw data:** 9 weeks, 255 total check-ins, 81% activation rate, 26% return rate, zero incentives.

**What can be calculated now:**

| Metric | Value | Notes |
|---|---|---|
| Activation Rate | **81%** | Best-in-class. Loyalty app typical onboarding: 30–45% |
| Weekly Check-in Rate | **~28 sessions/week** | 255 ÷ 9 weeks |
| Return Rate | **26%** | Must clarify window — 7/14/30 day? Changes interpretation |
| Completion Rate | **Unknown** | Not instrumented — add in Fall 2026 |
| Node Density | **Partial** | Need unique user count per week |
| Multi-Node Rate | **N/A** | Single node pilot — cannot calculate |
| Operator Decision Value | **Unknown** | Not tracked |
| Recognition Lift | **Unknown** | Recognition wasn't systematically varied |
| Revenue per Node | **$0** | Pilot is unpaid |
| Participation Compounding Score | **Incomplete** | Missing multi-node and completion data |

**What is unknown and must be measured in Fall 2026:**
1. Return rate window definition — 7/14/30 day?
2. Completion rate — do students who start a session always complete it?
3. Session frequency per user — avg sessions per activated user over 9 weeks
4. Cross-node transfer — impossible to test with one node
5. Recognition lift — cohort was never isolated
6. Operator decisions driven by data — Gully's didn't have a real dashboard
7. Unique user count vs. raw check-ins

**What the gaps reveal about what to instrument in Fall 2026:**
- Tag sessions by return window from day one — every session timestamped relative to each user's first session
- Define and track a "complete session" event separately from "scan"
- Build user-level session history across nodes, not just per-node aggregates
- Assign recognition cohorts — some users receive acknowledgment, some don't; measure the delta
- Create an operator decision log — even a Notion doc
- Add a gym node and one event node — the moment you have 3 node types, the compounding thesis can be tested

---

## 2D. Milestone Gates

**Gate 1: Single-Node Activation ≥ 70%**
**Status: PROVEN — 81% at Gully's**
- Threshold: 70% activation rate at any single node
- Unlocks: Confidence that students will scan without rewards. Removes the "why would they?" objection
- If missed: Zero-incentive model is broken — UX problem or wrong venue context

---

**Gate 2: 30-Day Return Rate ≥ 35% at Gully's**
**Target: Fall 2026, Week 4**
- Threshold: 35% of activated users return within 30 days of first session
- Unlocks: Evidence that presence habit is forming, not just novelty scanning. Justifies multi-node expansion
- If missed: Return behavior may be venue-driven, not Sway-driven. Recognition layer needs redesign

---

**Gate 3: Multi-Node Participation Rate ≥ 25% Across 3+ Nodes**
**Target: Fall 2026, Week 8**
- Threshold: 25% of active Sway users engage at 2+ distinct nodes within the same 30-day window
- Unlocks: The compounding thesis. This is what separates "app at a bar" from "participation graph." Unlocks the campus cluster pitch
- If missed: Students treat each node as a separate experience. The graph stays flat, and so does the business model
- Measurement requirement: Requires minimum 3 active nodes live simultaneously

---

**Gate 4: Operator Makes 1 Documented Decision from Sway Data**
**Target: Fall 2026, any point**
- Threshold: At least one operator takes a documented real-world action they attribute to Sway data
- Unlocks: The operator ROI story. Without this, Sway is a vanity dashboard
- If missed: Dashboard isn't surfacing actionable signal. Operators see data and shrug. The product is a check-in app, not an OS

---

**Gate 5: First Paying Node at $149+/Month**
**Target: January 2027 or earlier**
- Threshold: At least one node converts from free pilot to paid subscription
- Unlocks: Proof that someone will pay. Changes every investor conversation from "interesting experiment" to "early revenue"
- If missed: Willingness-to-pay assumption is unvalidated — either the value isn't real, the operator doesn't feel it, or the pricing framing is wrong
- Conversion rule: Do not ask for payment before Gates 2 and 4 are passed

---

## 2E. Investor Proof Points

| Metric | Threshold | Why It Lands |
|---|---|---|
| Activation rate, zero incentive | ≥ 70% | Disproves biggest loyalty/check-in objection — users won't scan without rewards |
| 30-day return rate, zero rewards | ≥ 35% | Loyalty industry pays $15–40 CAC to drive 20–30% return. Sway showing 35%+ without cost is defensible |
| Multi-node participation rate | ≥ 25% across 3+ nodes | Single-node return rate is impressive. Multi-node engagement is defensible infrastructure |
| Operator Decision Value | ≥ 3 decisions/month per node | Converts "vanity dashboard" to "operational tool" |
| Cluster ACV | ≥ $18,000 with 5+ nodes | Shows the institutional unit that makes campus roll-up story work |
| Cost per Node | ≤ $500 fully loaded | At $200/month revenue per node, payback under 3 months. Unit economics work |
| Participation Compounding Score | ≥ 0.10 | Single number telling investors the network is strengthening |

---

# Section 3: Pricing Strategy

---

## 3A. What Should Be Free During Pilot

**Gully's gets for free:**
- Unlimited session capture
- Basic operator dashboard — weekly active users, return rate, peak hour heatmap
- Student-facing recognition display (if built in Fall 2026)
- Hardware (QR placard or tap device) — Sway owns the hardware
- Onboarding and setup support

**Campus orgs / Endicott clubs get for free:**
- Session capture at events and meetings
- Basic community dashboard — attendance over time, new vs. returning members
- Sway identity integration (same student profile carries across nodes)

**Why free is correct right now:**

Free is not charity. Free is instrumentation.

1. **Data you can't afford to lose.** Fall 2026 is the semester that proves or disproves cross-node compounding. Every node that goes dark because of payment friction is a gap in the graph you can never recover.
2. **Dashboard habit formation.** Gully's needs to open the dashboard 12 times before they believe it. You cannot charge for a tool someone hasn't touched yet.
3. **Operator proof creation.** Gully's paying matters less right now than Gully's using data to make a real decision. That documented decision is worth more than $1,800 in ARR — it's the conversion story for every venue after them.
4. **Student density.** Thin graphs don't compound. Free nodes in Fall 2026 builds the user base that makes the product worth paying for in Spring 2027.

Free nodes cost Sway: hardware (~$30–80), Kev's time, server costs at this scale (negligible). That cost is justified by every data point collected.

---

## 3B. Pricing Tiers

**Tier 1: Single Venue / Node — $199/month**

Included:
- Unlimited session capture
- Operator dashboard: weekly active users, return rate trends, peak hour data, new vs. returning breakdown
- 90-day session history
- Weekly email digest
- Up to 500 monthly active users per node
- Standard QR or NFC setup (hardware included first 3 months)

Floor: $149/month for early adopters who sign before January 2027. Real discount, real expiration.
Ceiling: $299/month for venues with >500 MAU or operators who want weekly data calls.

---

**Tier 2: Student Organization / Community — $49/month**

Included:
- Session capture at up to 8 events/month
- Community dashboard: attendance trends, returning member rate, new member acquisition
- Member recognition feed (optional toggle)
- Integration with campus Sway identity

Logic: Campus orgs have no budget. $49 gets them on the graph and builds multi-node density without a lengthy sale. The value to Sway is the node, not the revenue. Consider: free in Fall 2026, $49 starting Spring 2027 after student profiles are already loaded.

---

**Tier 3: Campus Cluster Package — $1,500/month or $15,000/year**

Included:
- Up to 8 nodes (mix of venues, orgs, campus spaces)
- Cross-node participation dashboard — multi-node rate, power users, community overlap
- Operator-to-operator data sharing (anonymized)
- Cluster-level student identity graph
- Quarterly business review call
- Dedicated onboarding per new node
- Priority hardware support

Annual discount: $15,000/year = 2 months free. Gets institutions to commit before semester starts.

---

**Tier 4: Premium Analytics Add-On — $99/month per node**

Included:
- Raw session export (CSV/API)
- Custom cohort builder
- Churn prediction: users whose session frequency is declining
- Recognition ROI report: return rate delta for recognized vs. unrecognized cohorts
- Comparative benchmarking (anonymized network averages)

Gate: Only offer premium analytics after the operator has made at least 3 documented decisions from standard dashboard data.

---

**Tier 5: Institutional / Campus-Wide — Custom, starting $3,500/month**

What Endicott as an institution would pay — not individual venues, but the college itself.

Included:
- Unlimited nodes across campus
- Student affairs dashboard: campus-wide participation rates, community engagement scores, retention-correlated attendance patterns
- API integration with student information systems (future)
- Branded student identity experience
- Annual contract, invoiced quarterly
- Executive-level data presentations per semester

Pricing rationale: $3,500/month × 12 = $42,000/year ACV. For a 2,000+ student campus, that's $21/student/year — comparable to what schools pay for event management software that delivers far less behavioral signal.

---

## 3C. Pilot-to-Paid Conversion

**When to introduce the payment conversation:**
Do not have a pricing conversation until all three of these are true:
1. Gully's has 60+ days of Fall 2026 session data
2. The operator has opened the dashboard at least 8 times (trackable)
3. The operator can tell you — in their own words — one thing they learned from the data

Target window: Mid-October 2026, assuming Fall semester starts in early September.

**What to say when asking Gully's to pay:**

> "You've been on Sway for two months. You can see [X] students come through on [peak nights], and [Y]% of them have come back at least twice. We're moving to paid in January, and because you were our first partner, we want to keep your rate locked at $149 before we raise it. That's less than you spend on a single social media post that you can't measure. This tracks the real thing."

What NOT to say:
- "We're launching our SaaS platform"
- "We have a new pricing model"
- "We need to start charging to keep the lights on"

**How to phrase pricing so it doesn't sound like "another SaaS dashboard":**

Don't sell the software. Sell what they already know.

> "$199 a month. You know your Thursday crowd is different from your Saturday crowd — now you can see exactly who's coming back, how often, and when they stop. Cheaper than a part-time social media manager. You actually own the data."

Comparison anchors:
- Yelp ads: $300–$1,000/month, no behavioral data
- Toast marketing add-on: $75–$200/month, limited to transactions
- Instagram boosts: $200–$500/month, no retention measurement
- Doordash commission: 15–30% per order, no identity, no repeat tracking

**What Gully's paying proves to future venues:**
One paying customer is a price anchor. It tells every future venue: this is not a free beta, someone who used it decided it was worth paying for. The price point is $199/month.

Headline for every future pitch: "Gully's at Endicott College: 81% student activation, 26% return rate, now a paid Sway partner."

---

## 3D. What NOT to Charge For Yet

1. **Cross-node participation data for students** — Charging students to see their own history would kill activation. Students always see their own graph for free.
2. **Recognition features** — Build it, measure it, price it once the data shows it works. Charging for an unproven feature creates resentment.
3. **Event nodes and campus orgs** — Keep org nodes free through Fall 2026, convert Spring 2027 after student profiles are established.
4. **API or data export** — No one is asking for this yet. Save for the premium tier, delivered when operators request it.
5. **Anything requiring onboarding complexity** — If the feature requires a 30-minute training call, it's not ready to charge for.

---

## 3E. Pricing Psychology for Venue Operators

Bar and restaurant owners don't buy SaaS. They buy peace of mind, competitive edge, and outcomes they can explain to themselves at 1am when they're closing out the till.

**Their current spend, typically:**
- Yelp/Google ads: $200–$500/month → no repeat data
- Instagram/social: $200–$800/month → no behavioral signal
- Email list: $50–$150/month → low open rates, no venue-level behavior
- Loyalty punch cards: free to print, near-zero redemption, no data

**Three anchors that land with bar operators:**

1. **The staff anchor:** "Your bartenders already recognize regulars. This is just that, but for the 60% of people who come in once and you never see again."
2. **The Wednesday problem:** "Every bar has a dead Wednesday. Sway tells you if it's dead because your regulars aren't coming, or because you're not getting new people. Different problem, different fix."
3. **The comp anchor:** "One wasted keg or one over-staffed slow night costs you more than $199. Sway tells you which nights to staff up before they happen."

**What not to say:** "Participation OS," "identity graph," "SaaS platform," "actionable insights," "student engagement metrics."

**What lands:**
- "You'll know who's coming back and who's gone cold."
- "You'll see your busiest night before it happens."
- "You'll know if a new event actually worked."
- "$199/month. Cheaper than the Instagram ads that don't track this."

The close is simple: they've seen the data for 60 days. Ask them what they'd do differently if they didn't have it. Whatever they say — that's what $199 buys.

---

# Section 4: Business Model Risks

*For each risk: why it matters, how to test it, what metric confirms or denies it, what to do if confirmed.*

---

## Risk 1: Students Do Not Develop a Repeat Check-In Habit

**Why it matters:** The 26% return rate is a headline number. If most returners came back exactly once more and stopped, Sway captured a novelty effect, not a behavior change. The entire operator value proposition — regulars identification, programming insight — collapses if there are no regulars.

**How to test it:** Pull the raw session distribution from Gully's. Count users by total session count: 1, 2, 3, 4, 5+. Look for a power-law tail.

**Metric that confirms or denies it:** ≥20% of activated users complete 3+ sessions within the pilot window. Below 10% = novelty hypothesis wins.

**Response if confirmed:** Shift product design toward habit scaffolding — session milestones, identity signals that accumulate visibly. Do not add rewards. Add memory.

---

## Risk 2: QR Check-Ins Are Too Weak as Identity Infrastructure

**Why it matters:** QR codes are gameable, forgettable, and depend on placement/visibility. If the session capture mechanism is unreliable, data quality degrades, operators lose confidence, and the participation graph is polluted with false sessions.

**How to test it:** Audit Gully's scan data for anomalies — scan clustering in non-peak hours, multiple scans from same device in a short window. Interview 10–15 students about the scanning habit.

**Metric that confirms or denies it:** <10% of sessions show anomaly signals. Student recall rate in interviews: ≥70% describe scanning as intentional and self-directed.

**Response if confirmed:** Layer passive signal on top of QR — NFC tap, geofence confirmation. QR becomes one of multiple session confirmation signals, not the only one.

---

## Risk 3: Operators Like the Data But Won't Pay

**Why it matters:** This is the most common death of a free analytics tool. Operators use the dashboard, find it interesting, but treat it like weather.com — nice to know, not worth paying for. Zero revenue from operators means the SaaS model doesn't work.

**How to test it:** Before the Fall 2026 pilot, have the paywall conversation directly. Tell Gully's: "This fall, we're converting to paid. Here's the pricing." Observe the reaction.

**Metric that confirms or denies it:** At least one venue commits to a paid contract before Fall 2026 launch, or agrees to a defined pilot-to-paid conversion at a named date. Verbal "yeah, probably" does not count.

**Response if confirmed:** Reframe the product. If operators won't pay, find who will — campus administrators buying programming insight, student life offices buying engagement data. The data is valuable; the buyer may not be the venue.

---

## Risk 4: Campus Churn from Annual Student Turnover

**Why it matters:** 25% of the student body graduates every year. New first-year students arrive every fall with no relationship with Sway. The user base constantly resets. The venue stays, the students don't.

**How to test it:** Track Fall 2026 activation rate separately for new students vs. returning students.

**Metric that confirms or denies it:** Returning student activation rate ≥60% within 2 weeks of semester start without a dedicated re-engagement campaign. New student activation rate ≥50% within 4 weeks.

**Response if confirmed:** Build identity continuity — returning students see their Spring history immediately. Design a "welcome back" moment. Add an ambassador layer (student employees, RAs, club leaders) for new student acquisition.

---

## Risk 5: SaaS-Only Market Is Too Small for Venture Scale

**Why it matters:** At $149–$299/month per venue, reaching $1M ARR requires 280–560 paying nodes. Reaching $10M ARR requires 2,800–5,600. That number of nodes across fragmented campus markets is a 7–10 year build. Investors writing $2M+ checks want a path to $50M+ ARR.

**How to test it:** Model the campus cluster unit. If a single campus of 3,000 students has 8–12 nodes and the package price is $1,500–$3,000/month, what does the TAM look like at 500 campuses?

**Metric that confirms or denies it:** One cluster deal at $2,000+/month is more valuable to the investor story than ten individual venue deals at $199.

**Response if confirmed:** Move cluster pricing to the front of the pitch. The per-node model is a wedge, not the model. Add institutional buyers (university admin, student affairs) as a parallel revenue channel.

---

## Risk 6: Too Many Node Types Dilute Focus

**Why it matters:** Campus bar + gym + club event + sports game + off-campus restaurant = five different contexts. Different scan surfaces, different staff involvement, different operator dashboards needed. A 2–5 person team cannot build excellent products for five use cases simultaneously.

**How to test it:** Before adding a second node type, define the exact integration requirement for the new context. Does it require new hardware? New student UX? New operator dashboard views?

**Metric that confirms or denies it:** A second node type activates at ≥70% of the Gully's activation rate using the same product, no custom development. If it requires >20 hours of engineering to make a new context work, the abstraction is wrong.

**Response if confirmed:** Enforce a single-node-type discipline through Fall 2026. Campus bar or campus venue is the type. Build the abstraction layer that makes expansion cheap before expanding.

---

## Risk 7: Dashboard Does Not Change Operator Behavior

**Why it matters:** Data ≠ decisions. If Gully's manager looks at the heatmap, shrugs, and does what they were already doing — there is no demonstrated value chain, no willingness to pay, no renewal story.

**How to test it:** Run a structured operator interview mid-semester: "In the last 30 days, name one staffing, programming, or promotional decision you made because of what you saw in Sway."

**Metric that confirms or denies it:** ≥1 documented operator decision change per month, correlated with a measurable outcome.

**Response if confirmed:** Stop building features. Start embedding. Sit with the operator once a week for 30 minutes and read the dashboard together. Turn data into weekly operator recommendations. Build that into the service layer first, then automate it.

---

## Risk 8: Sway Accidentally Becomes a Loyalty or Discount App

**Why it matters:** Operators, under pressure to justify product cost, ask for perks and rewards. Sway adds them. Students start expecting them. The product is now a loyalty app competing with Thanx and Blackbird on their turf. Differentiation disappears.

**How to test it:** Track how many operator conversations include a rewards request within the first three months of any pilot.

**Metric that confirms or denies it:** Zero rewards features shipped. Operator retention at renewal without any incentive mechanics. If Sway cannot retain a venue without adding rewards, the product has not proven its standalone value.

**Response if confirmed:** "We don't do rewards because that's Thanx. We do recognition — the student knows you know them. That's different." If the operator still needs rewards to justify the product, they are not the right customer. Filter them out.

---

## Risk 9: Payments Introduced Too Early

**Why it matters:** Investor pressure or revenue targets push Sway to add payments before identity density is proven. Engineering focus splits. The identity story gets muddied. The company is doing two hard things at once, neither well.

**How to test it:** Track how many inbound product conversations are about payments vs. identity/recognition.

**Metric that confirms or denies it:** Sway does not ship any payments feature until: (a) ≥3 campuses are live, (b) ≥1 campus cluster has renewed once, and (c) ≥50% of active venues report unprompted that they want payments added.

**Response if confirmed:** Create an explicit internal product gate. "No payments discussion until [milestone]." Use it as an investor filter — if a check writer requires payments in Year 1, they don't understand the thesis.

---

## Risk 10: Network Effects Don't Emerge

**Why it matters:** The venture-scale story requires network effects. Without them, Sway is a multi-location SaaS tool with per-node pricing. Any competitor with more marketing budget can replicate it.

**How to test it:** With 2+ nodes live, measure cross-node participation: what percentage of students who scan at Node A also scan at Node B within the same semester?

**Metric that confirms or denies it:** ≥25% of active users engage with ≥2 nodes by end of first multi-node semester. Average sessions per user increases as node count increases.

**Response if confirmed:** The product needs an explicit cross-node discovery mechanic. Not a social feed. A student identity page that shows participation across the campus: "You've been to Gully's 4x, the gym 9x, and 2 club events this semester." The graph becomes visible to the student, which creates the motivation to build it.

---

## Risk 11: Academic Calendar Creates Perpetual Restart Problem

**Why it matters:** August through May is the operating window. June and July are dead. Every August is a re-launch. Investors modeling SaaS businesses expect MRR that grows month over month. Sway's MRR structure is inherently seasonal.

**How to test it:** Project the MRR curve month-by-month for 24 months. What does August churn look like? Is it a pause (venue contract continues, students go home) or true churn?

**Metric that confirms or denies it:** If venues sign 12-month contracts regardless of student calendar, summer is a cash flow non-issue. If venues demand to pause or cancel in summer, the business has a structural revenue problem.

**Response if confirmed:** Price for the academic year, not the calendar year. $1,800 billed annually (September–May, 9 months) structured as a 12-month contract with summer as included downtime. Frame summer as the data analysis and re-onboarding period. Charge for it anyway.

---

## Risk 12: Student Privacy and Data Perception

**Why it matters:** One viral "this app is tracking you" social post ends a campus partnership instantly. University administration can pull access without notice. The press narrative writes itself. It doesn't have to be accurate to be damaging.

**How to test it:** Run a student perception survey: "How comfortable are you with a venue app that records your check-ins?" Measure comfort levels before and after explaining how data is stored.

**Metric that confirms or denies it:** ≥80% of surveyed students describe Sway as "remembering" or "recognizing" rather than "tracking" or "watching." Zero privacy complaints escalated to university administration in first semester.

**Response if confirmed:** Make data ownership explicit and student-facing. Students can see their data, delete their data, and export their history. Frame the product as a personal participation record — the student owns the graph, the venue gets aggregated signal only.

---

## Risk 13: No Defensible Moat at the Node Level

**Why it matters:** A QR code on a wall, a scan counter, and a basic dashboard is not a hard product to replicate. A funded competitor can add a campus check-in feature in a sprint. Without structural lock-in, churn accelerates the moment a competitor shows up.

**How to test it:** Audit what a venue would lose if they switched to a competitor after one semester. Is the participation history portable to the new system? Is there anything painful to replicate?

**Metric that confirms or denies it:** Identify at least two structural lock-in mechanics before the end of Fall 2026 (participation history living in student's Sway identity, campus cluster contracts requiring multi-node switching simultaneously, benchmark data requiring 12+ months of history).

**Response if confirmed:** Build moat into the data layer, not the feature layer. The participation graph — a student's history across nodes, semesters, and venues — is not replicable by a competitor who shows up six months later.

---

## Risk 14: Founder Dependency on Single Pilot Relationship

**Why it matters:** Gully's is the only live signal. If that relationship changes — manager leaves, ownership changes, venue closes — Sway loses its only proof point before Fall 2026.

**How to test it:** Map the Gully's relationship today. Who is the operator contact? Who is the decision-maker on contract renewal? If the answer to both is one person, the relationship is fragile.

**Metric that confirms or denies it:** At least 2 named stakeholders at Gully's understand and advocate for Sway independently. A written pilot agreement for Fall 2026 before summer ends. A second venue in conversation before September.

**Response if confirmed:** Begin outreach to a second campus venue before August. It does not need to be a paid contract — a committed Fall pilot at a second location changes the risk profile from "one relationship" to "repeatable process."

---

# Section 5: Investor Readiness Checklist

---

## 5A. Product Proof

**What must the product demonstrate:**
- Physical presence captured reliably without staff involvement
- Student-facing session history that accumulates and is visible to the user
- Operator dashboard with meaningful cohort and behavioral data, not just a scan counter
- Multi-node capability — the same student appearing across different venues in the same network

| Capability | Status |
|---|---|
| Presence captured without staff involvement | **PROVEN** |
| Basic scan event logging | **PROVEN** |
| Operator dashboard with session frequency data | **IN PROGRESS** |
| Student-visible participation history accumulating over semesters | **NOT YET PROVEN** |
| Multi-node session tracking | **NOT YET PROVEN** |
| API or data portability layer | **NOT YET PROVEN** |

---

## 5B. Behavior Proof

| Signal | Threshold | Status |
|---|---|---|
| Single-venue activation rate | ≥ 60% | **PROVEN** — 81% at Gully's |
| 30-day return rate | ≥ 20% | **PROVEN** — 26% with zero incentives |
| Users with 3+ sessions | ≥ 20% of activated users | **NOT YET PROVEN** — distribution not reported |
| Users with 5+ sessions | ≥ 10% of activated users | **NOT YET PROVEN** |
| Multi-node participation | ≥ 1 user across 2+ nodes | **NOT YET PROVEN** — only one node exists |

**The most important missing data point:** Session frequency distribution from Spring 2026. Pull this before Fall begins.

---

## 5C. Multi-Node Proof

**What must be true for the campus cluster thesis to be credible:**
- At least 2 nodes live on the same campus simultaneously
- A measurable percentage of students visit both nodes in the same semester
- Operator data shows cross-node cohort behavior
- A single campus administrator can see the cross-node view in one dashboard

**Current status: NOT YET PROVEN** — zero multi-node data exists. Fall 2026 must include at least one second node.

---

## 5D. Operator Value Proof

| Signal | Status |
|---|---|
| First paid venue contract | **NOT YET PROVEN** |
| Documented weekly dashboard usage | **IN PROGRESS** — Gully's engagement not formally tracked |
| Operator names specific decisions made from data | **NOT YET PROVEN** |
| Renewal after one full academic year | **NOT YET PROVEN** |

---

## 5E. Willingness-to-Pay Proof

**Minimum evidence needed:**
- One venue signs a contract with a dollar figure before services are delivered
- Pilot-to-paid: Gully's moves from free to paid in Fall 2026 at any price point, with a signed agreement

**What counts as interview evidence:**
- Operator compares Sway favorably to a tool they currently pay for (strong)
- Operator asks "how do we set this up for next semester" before price is discussed (strong)
- Operator is presented with specific pricing and does not immediately decline (medium)
- Operator says "I would pay for this" unprompted (weak — words are cheap)

**What counts as transaction evidence:** Wire transfer, card charge, or invoice paid. Nothing else.

**Current status: NOT YET PROVEN.** This is the most critical gap before any investor conversation at seed stage.

---

## 5F. Retention and Lift Proof

**What cohort data would demonstrate recognition → repeat:**
- Split the Spring 2026 cohort by session count (1 session, 2–3 sessions, 4+ sessions)
- Show that higher session-count students also showed higher return rate in weeks 5–9 vs. weeks 1–4
- If recognition is the mechanism, users who received any in-product identity signal should show higher return than those who did not

**Current status: IN PROGRESS** — raw data exists from Spring 2026 but has not been analyzed at cohort depth. This analysis must be completed before Fall 2026.

---

## 5G. Expansion Proof

**What makes a second campus credible:**
- The second venue was acquired without a pre-existing founder relationship
- The second campus activates at ≥60% of the Gully's activation rate without on-site founder involvement
- The playbook is documented and followed by someone other than the founder

**Current status: NOT YET PROVEN** — only one venue exists.

---

## 5H. Current Investor Readiness Assessment

**What Sway has right now:**
- A live pilot with real behavioral data: 255 check-ins, 81% activation, 26% return, zero incentives
- A clean thesis with clear differentiation from loyalty/rewards category
- A thesis-consistent founding insight: students participate without being bribed
- A real venue partner who did not churn during the pilot
- A defined expansion path (campus cluster) with plausible unit economics

**What a pre-seed investor wants:**
- Evidence that at least one customer would pay something for the product
- Depth data on the pilot (not just headline activation — session distribution, cohort curves)
- A replicable wedge
- A founder who can explain precisely why this is a venture business, not a lifestyle SaaS

**What a seed investor wants:**
- ≥1 paying venue with a signed contract
- ≥2 campuses live or signed
- Session depth data showing habitual use (3+ sessions per user in meaningful percentages)
- Multi-node participation emerging
- Documented operator behavior change from dashboard data
- A path to $1M ARR with visible mechanics

**The honest gap:**
Sway is at the back half of pre-seed evidence. The behavioral proof (81% activation, 26% return with zero incentives) is genuinely strong. The gaps are: zero paid revenue, no depth analysis on session distribution, no multi-node data, no second campus.

**What Fall 2026 closes:**
If Fall 2026 produces (1) Gully's on a paid contract at any price, (2) one second node live at Endicott, (3) session depth analysis from Spring showing ≥20% of users hit 3+ sessions, and (4) one operator interview where they name a specific decision made from Sway data — Sway exits Fall 2026 at the front of the pre-seed range and enters seed conversations with a credible story.

If Fall 2026 ends with Gully's still free and still the only venue, the seed round is at least one more semester away.

---

# Section 6: 90-Day Business Model Validation Plan — Fall 2026

---

## Weeks 1–2: Baseline + Gully's Reboot

**Goals**
- Gully's live on Day 1 of the semester
- Spring 2026 data fully segmented before the first new check-in happens
- Cohort baselines established so Fall data has something to compare against

**Key Actions**

*Data work (complete in August before students return):*
- Pull all Spring 2026 sessions from Supabase. Segment into four cohorts: 1x, 2x, 3x–4x, 5x+ visitors
- For the 5x+ cohort: calculate average days between visits, identify peak visit windows (day of week, time of day), flag any who visited 3+ consecutive weeks
- For the 2x cohort: identify time gap between visit 1 and visit 2 — this is your conversion window
- Document the frequency distribution curve. What % of unique users had 1 session, 2 sessions, 3+?
- Flag the top 10% by session count — re-acquire these users in week 1 of Fall

*Student interviews (3–5 students, recruited via DM before they return):*
- 2 students from the 5x+ cohort — Why did you keep coming back? Did you think about Sway between visits?
- 2 students from the 1x cohort — Why didn't you return? Did you remember the app?
- 1 student who activated but never returned — What did the app feel like when you first scanned?
- Looking for: Is return behavior driven by the venue, the product, or social context?

*Setup:*
- Confirm QR placement at Gully's with the manager before semester starts
- Ensure Supabase dashboard is clean, segmented, and ready to read Week 1 numbers without manually pulling data
- Create a tracking doc: daily check-ins, daily new users, daily returning users. Update weekly

**Success Metrics**
- Gully's live Day 1 of the semester
- Frequency distribution from Spring documented before Week 1 ends
- Know which cohort to target for re-acquisition

---

## Weeks 3–4: Add Node 2 and Node 3

**Goals**
- Second and third node live — not perfect, live
- Begin generating cross-node participation data

**Key Actions**

*Node selection logic:*
- Node 2: Campus gym — highest ambient student traffic, daily habit venue, no persuasion required. Ask: "Would you want to know which students are your actual regulars vs. people who came once?" QR up that week. Five minutes of their time.
- Node 3: Foundry / Angle Center or Entrepreneurship Club — whichever has a scheduled event in weeks 3–4. Ask: "You ran Pitch Night. We can tell you whether the students who came ever came back to the Foundry." 
- Do not add all five nodes at once. Two new nodes is enough signal. Three is noise you can't diagnose.

*What to watch:*
- Primary signal: What % of Gully's Spring users check in at Node 2 or Node 3 within the first two weeks?
- Secondary signal: Do Node 2/3-first users then visit Gully's?
- This cross-pollination rate is your participation graph signal

**Success Metrics**
- Multi-node participation rate of ≥15% within first two weeks of each node going live
- At least one student who checked in at Gully's also checks in at Node 2 or 3
- Cross-pollination is documented, not just observed

---

## Weeks 5–6: Sway Card + Status Launch

**Goals**
- Recognition layer active without making it feel like a loyalty program
- Test whether visible identity changes return behavior

**Key Actions**

*What Sway Card is:*
- A student's portable participation record: where they've shown up, how often, their regular status at specific venues
- Not a punch card. Not a rewards card. A social artifact.
- The signal it sends to a student: "You're a regular here. Sway knows it. Now you can show it."

*How to introduce status without making it a loyalty program:*
- Do not announce it as a rewards launch. Do not email "you've earned X points."
- Surface it passively: when a student checks in for their 3rd time, they see their status update. No fanfare, no email blast.
- At Gully's: tell the manager there's a "regular" indicator — ask them to acknowledge it when a student shows it. Not a discount, a moment of recognition. "Hey, I see you're a Gully's regular."
- Language to avoid: loyalty, points, rewards, earn, redeem, tier. Language to use: regular, recognized, remembered, your record, where you've been.

*What to watch for:*
- Screenshots shared to Instagram/group chats (organic proof)
- Students showing the card to friends or the bartender unprompted
- Return rate increase in the 14 days after card launch vs. the same cohort's 14-day return rate pre-launch
- Watch the 2x cohort specifically — does the card push them to a 3rd visit?

**Success Metrics**
- Measurable lift in 14-day return rate for the cohort that received status, vs. the pre-status baseline from Weeks 1–4
- At least 3 documented instances of students showing or sharing their card

---

## Weeks 7–8: Dashboard Review with Operators

**Goals**
- Sit down with Gully's manager and Foundry/E-Club organizer
- Show them data that helps them make a real decision
- Document what they act on — this is proof that operator value is real

**Key Actions**

*What to show Gully's manager:*
- Your regulars: here are the 20 students who showed up 5+ times. These are your actual loyal customers — not your biggest spenders, your most frequent visitors.
- Event-to-return: you ran [X night] in Week 4. Here's how many people who came to that event returned within 14 days. Here's how many didn't. What does that tell you about that night?
- Cross-node data: here are students who checked in at Gully's and at the gym. They're your highest-probability regulars.
- Gap analysis: here are students who visited twice but stopped. What happened?

*What to show Foundry/E-Club:*
- Event attendance vs. ongoing engagement: how many people who came to Pitch Night checked in again at any Sway node in the following 3 weeks?
- Which students are showing up across multiple campus touchpoints? These are your most engaged students.

*The decision you want them to make:*
- Gully's: "Based on this data, are you going to do anything differently with [specific night or programming]?"
- Foundry: "Would knowing this before your next event change how you invite or follow up with students?"
- You are not asking them to renew or pay. You are asking them to act on data. If they act, you have proof of value.

*Document it:* Write down what they said. Write down what they decided. Take a photo if they pull out a pen and circle something on the screen. This becomes the case study.

**Success Metrics**
- At least one operator makes a documented programming or operational decision based on Sway data
- You have a quote from at least one operator about what surprised them

---

## Weeks 9–10: Test Willingness to Pay

**Goals**
- Have the pricing conversation with Gully's
- Surface what must change before they say yes, if they say no

**Key Actions**

*How to frame it:*
> "We're moving from the pilot to our regular model in the spring. For venues like Gully's, it's $149/month. What you're getting is [name the specific things you showed them in Weeks 7–8 that they cared about]. Given what you saw in the data, does that make sense?"

*Objections and responses:*
- "I don't control the budget" → Find out who does. You need the budget owner in the next conversation.
- "It's not in the budget this semester" → "What would have to be different? What's the specific threshold?"
- "We can keep doing this for free, right?" → "The pilot was free to run the research. The product going forward is $149/month. What would make $149 an easy yes?"
- "I need to think about it" → "What would you need to see that you haven't seen yet?" Then go build that proof.

*What the prior 8 weeks give you in this conversation:*
- Real data, not hypotheticals
- A decision they already made using Sway data — you can point to it
- A pattern of zero friction (no staff changes, no customer confusion)
- A 26% return rate baseline they know is real

**Success Metrics**
- At least one node is paying OR you have a specific, documented set of conditions that must be met before they pay
- The conversation happened — no delaying it

---

## Weeks 11–12: Package the Cluster Case Study

**Goals**
- Document Endicott as the proof-of-concept campus cluster
- Make this usable for the YC application, the Dean of Business pitch, and the next campus partner conversation

**Key Actions**

*What the case study includes:*
- Before: What Gully's knew before Sway
- After: Specific numbers — 255 check-ins, 81% activation, 26% return rate, top 20 regulars identified, cross-node participation stats, one operator decision made
- Node map: Endicott as a campus cluster — Gully's + gym + Foundry/E-Club
- Quote from Gully's manager
- Multi-node stat: X% of Sway users participated at 2+ campus nodes during Fall 2026

*Who it's for:*
- YC: proof of participation density in a single campus cluster. The question YC will ask is "does this compound?" Your answer is the multi-node graph.
- Dean of Business / Endicott admin: student engagement visibility they've never had.
- Next campus partner: replication pitch. "We did this at Endicott. Here's what the first semester looked like."

*Decision points:*
- Multi-node participation rate >20%: double down on campus cluster model, accelerate second campus pitch
- Gully's pays or commits: you have unit economics, go raise
- Cross-node data weak (<10%): the cluster thesis needs work, single-venue model may be what's working

*Kill criteria — what would make you rethink the campus wedge:*
- Return rate at Gully's in Fall materially lower than Spring (<15%) without clear explanation
- Zero operator willingness to pay after 10 weeks of live data and a real pricing conversation
- No cross-node participation after 4+ weeks of two active nodes
- Students describe Sway as "the check-in app" with no awareness of the identity or recognition layer

---

# Section 7: Sales Motion

---

## A. Gully's (On-Campus Bar)

**Buyer:** General Manager or ownership  
**User:** Bar staff (passively), returning students (actively)  
**Champion:** The GM already in relationship with Sway  
**Budget owner:** GM or ownership group — confirm before Week 9 conversation  
**Pitch:** "You've spent 10 weeks knowing exactly who your regulars are and which nights actually create loyal customers. That's the product. It's $149/month."  
**Proof needed:** The data they've already seen. The decision they already made in Week 7–8.  
**Likely objections:**
- "I don't control the budget" (ownership does)
- "It's been free" (the pilot was a research phase)
- "Our students are already loyal" (no — you know who's actually loyal, and it's fewer than they think)

**Close condition:** Ownership is in the room, they've seen the regulars list, and you've connected $149 to a decision they already made using Sway data.

---

## B. Off-Campus Venue (Bar / Restaurant Within 2 Miles of Campus)

**Buyer:** Owner or GM  
**User:** Bar staff (passive), students (active)  
**Champion:** None yet — create one. Start with the person who already talks to Endicott students regularly.  
**Budget owner:** Owner  
**Pitch:** "Endicott students are your most consistent Tuesday/Thursday night segment. We can show you who keeps coming back versus who visited once — and whether your college nights are building real loyalty or just foot traffic."  
**Proof needed:** Gully's case study — specifically the return rate and regulars identification.  
**Likely objections:**
- "Students already come here" (yes, but you don't know which ones come back)
- "We don't have time to manage another app" (you don't manage anything — one QR, nothing else)
- "How is this different from Yelp or Instagram?" (those tell you what people say. This tells you who actually comes back)

**Close condition:** Owner sees a specific student segment they want to understand better and believes the QR will be used (show Gully's activation rate as proof).

---

## C. Campus Student Organization (E-Club, Sports Team, Club)

**Buyer:** Faculty advisor or department head  
**User:** Club members, event attendees  
**Champion:** Club president or the student who already cares about engagement metrics  
**Budget owner:** Faculty advisor controls student activity funds — check if there's a department budget  
**Pitch:** "You run events. You want to know if they're building an actual community or just getting people in the door once. Sway tells you who came back after your last event — and who your most engaged members actually are."  
**Proof needed:** Event-to-return data concept explained simply. One example from Gully's adapted to the event context.  
**Likely objections:**
- "We already take attendance" (attendance is presence. Sway is return behavior.)
- "We can't pay for software" (find what budget they have, or position as free in exchange for data and testimonial)
- "Students won't scan" (81% activation at Gully's without any incentive)

**Close condition:** Faculty advisor is bought in, club president is excited, there's a scheduled event in the next 3 weeks to deploy around.

---

## D. Foundry / Angle Center

**Buyer:** Director of the Foundry or Angle Center  
**User:** Student entrepreneurs, program participants  
**Champion:** Program director or whoever runs the day-to-day calendar  
**Budget owner:** Director — likely has discretionary program budget  
**Pitch:** "You want to know which students are actually engaged in the entrepreneurship ecosystem versus who showed up once. Sway gives you a participation graph across every event and visit — so you can find your real community and prove program ROI to administration."  
**Proof needed:** The concept that participation breadth predicts real engagement. They care about program impact metrics for reports to the Dean.  
**Likely objections:**
- "We have a CRM for this" (a CRM tracks registrations, not actual physical presence)
- "Administration would need to approve this" (escalate early — bring them into the Endicott institutional pitch)

**Close condition:** Director sees how Sway data supports their end-of-year impact report to the Dean, and they have budget authority or Dean buy-in.

---

## E. Endicott Administration (Dean, Retention Office)

**Buyer:** Dean of Business or VP of Student Affairs  
**User:** Administrative staff, student success advisors  
**Champion:** Gina Deschamps (already engaged); new Dean of Business (in progress via President Cain)  
**Budget owner:** Dean or VP level — institutional budget, likely $5,000–$15,000/year  
**Pitch:** "You know which students are enrolled. You don't know which students are actually showing up to campus life. We can show you a participation graph across Gully's, the gym, the Foundry, and campus events — so you know who's engaged and who might be at risk before it shows up in retention data."  
**Proof needed:** The Endicott cluster case study. Multi-node data. A clear framing connecting participation to retention (students who participate in campus life retain at higher rates — established research).  
**Likely objections:**
- "We have survey data for this" (surveys tell you what students say. Participation data tells you what they do.)
- "FERPA concerns" (address proactively — Sway is opt-in, no academic data, have a one-pager ready)
- "We'd need to go through procurement" (yes — start conversation in November, budget cycles for next academic year)

**Close condition:** Dean sees the participation graph for their campus, connects it to a retention or engagement metric they already care about, and has a path through procurement or discretionary budget.

---

## F. Second Campus (Replication Pitch)

**Buyer:** Dean of Students, Dean of a specific school, or Director of Student Life  
**User:** Students, campus venue operators, clubs  
**Champion:** Need a warm intro — ideally through President Cain network, YC alumni network, or a student at the target campus  
**Budget owner:** Institutional budget, same as above  
**Pitch:** "We ran a 9-week pilot at Endicott College — 255 check-ins, 81% activation, 26% return rate, zero marketing, zero incentives. We can do the same at your campus starting this spring. Here's what the Endicott participation graph looks like."  
**Proof needed:** The packaged Endicott case study. Multi-node data. An operator quote. Gully's willingness-to-pay outcome.  
**Likely objections:**
- "How do we know students at our campus will use it?" (same as Endicott — QR, no friction, no incentive needed)
- "We'd want to see it run for a full semester first" (Endicott is now your full semester proof)

**Close condition:** Decision-maker has seen the Endicott case study, has an internal champion, and there's a semester start in the next 90 days to deploy around.

---

# Section 8: Strategic Partner Map

---

## A. Endicott College / Angle Center

**What they provide:** Physical infrastructure, institutional legitimacy, access to the student body, warm introductions to administration, the first campus cluster proof point.

**What Sway gives them:** Student participation visibility across campus life, data to support retention and engagement programs, a modern proof point for the Angle Center's innovation mission.

**What risk they reduce:** Reduces Sway's need for cold outreach on campus — every new node at Endicott is a warm institutional add, not a cold sale. Reduces investor skepticism about whether institutions will actually partner.

**When they matter:** Now through Fall 2026 and beyond. President Cain and Gina Deschamps are active relationships — do not let them go cold over summer.

---

## B. Gully's

**What they provide:** The live venue, the Spring 2026 data set, the first real operator relationship, and — if they pay — the first proof of willingness to pay.

**What Sway gives them:** Regulars identification, event-to-return data, cross-node overlap with campus gym and Foundry users, recognition infrastructure.

**What risk they reduce:** Gully's is proof the product runs without staff disruption. Every skeptical venue operator asks "does this require training?" Gully's answer is no.

**When they matter:** Critical now. The Fall 2026 willingness-to-pay conversation is a forcing function. If they pay, everything accelerates. If they don't, you learn exactly what must change.

---

## C. Campus Gym / Athletics

**What they provide:** Highest ambient daily traffic on campus — more frequent than any bar or event space. Adds a non-nightlife node, expanding the participation graph to a different behavioral context (habit vs. social).

**What Sway gives them:** Actual usage data beyond swipe-in counts. Who are the real regulars? Which students go 3x/week vs. visited once in September?

**What risk they reduce:** The gym node proves Sway works outside alcohol-adjacent contexts. This matters for the institutional pitch — Deans do not want their campus participation data tied only to a bar.

**When they matter:** Weeks 3–4 of Fall 2026. Get this node live early — it provides the cross-node data needed for the Weeks 7–8 dashboard review.

---

## D. Student Organizations (E-Club, Sports Teams)

**What they provide:** Event-based session data, peer-to-peer distribution, and community validation that Sway is for campus life broadly, not just bars.

**What Sway gives them:** Event ROI data — did the people who attended your event come back? Which members are actually engaged? Leadership identification.

**What risk they reduce:** Reduces the "Sway is just for drinking" perception risk. The Entrepreneurship Club in particular becomes an ambassador if they believe in the product.

**When they matter:** Weeks 3–6 of Fall 2026 for initial nodes.

---

## E. Off-Campus Student-Heavy Venues

**What they provide:** Revenue outside the institutional model (venues pay independently, no college budget process), proof the model works beyond campus infrastructure.

**What Sway gives them:** The Endicott student segment identified as a distinct, trackable customer base. Knowledge of which nights drive real repeat behavior vs. one-time traffic.

**What risk they reduce:** Reduces single-customer concentration risk. A paying off-campus venue proves the SaaS model works outside institutional deals.

**When they matter:** Weeks 9–10 of Fall 2026 for willingness-to-pay conversations. Prioritize one off-campus venue first.

---

## F. Technology Partners

**Supabase (current):** Core database, auth, and realtime infrastructure. Protect this stack. Do not introduce competing infrastructure.

**NFC hardware (future):** QR is the right entry point today. NFC becomes relevant when you have enough venue density to justify hardware logistics. The trigger: when QR friction becomes a documented drop-off reason — not before. Target partner type: established vendor who already sells into hospitality.

**Apple Wallet / Google Wallet integration (future):** Sway Card living in Apple Wallet is a high-value unlock — makes the identity layer visible outside the app, removes "open the app" friction. Build the in-app card now; port to Wallet in Spring 2027.

**When they matter:** NFC hardware — not before second campus. Apple Wallet — after Fall 2026 data validates the Sway Card as a meaningful identity signal.

---

## G. Payment Partners (Phase 4 Only)

**Do not build this now.** The right payment partner — when Phase 6 arrives — is a hospitality-native partner who already has venue relationships and wants session context attached to transactions. Think: a company like Revel, Toast, or a campus ID system that handles closed-loop spending. The trigger: operators asking "can students pay through Sway?" That question does not exist yet.

**When they matter:** Phase 4. Not before proven identity density across at least one full campus cluster.

---

## H. Legal / Privacy Advisors

**What they provide:** FERPA compliance framing, age verification guidance for bar nodes, student data privacy policy language, protection against the first institutional partner who sends your terms to their legal team.

**What Sway gives them:** A clean, early-stage client with a novel data model.

**What risk they reduce:** FERPA risk is the most common objection from Deans and Student Affairs offices. A one-page privacy summary from legal counsel — not a founder — closes that objection before it stalls a deal. Have this ready before you're in that room.

**When they matter:** Before the Endicott institutional pitch to the Dean. Not after.

---

# Section 9: What to Do Next — Priority List
*June 15 – Mid-August 2026*

**1. Run the full Gully's cohort analysis**
Why now: Fall 2026 strategy depends on knowing exactly what happened in Spring — who converted, who didn't, what the frequency curve looks like. Done when: 1x / 2x / 3x / 5x+ cohorts are documented, top 10% are identified, average return window for multi-visit users is calculated.

**2. Interview 5 students before they scatter**
Why now: Student memory of why they used Sway (or didn't) degrades fast. You need qualitative signal before Fall decisions are locked. Done when: 2 high-frequency users, 2 single-visit users, and 1 activated-but-never-returned user have been interviewed.

**3. Confirm Gully's Fall 2026 relationship in writing**
Why now: You need a written pilot agreement for Fall before summer ends, and you need to know who the actual budget owner is before the Week 9 payment conversation. Done when: meeting happened, Fall launch confirmed, and you have one sentence from them about what they found useful in Spring.

**4. Book a meeting with Gina Deschamps before August**
Why now: The Endicott institutional relationship needs a move before summer ends, and Gina is your current warm path to the Dean of Business. Done when: meeting is scheduled. Bring the Spring data and a one-page "what Fall looks like" summary.

**5. Get in front of the new Dean of Business**
Why now: President Cain has opened the door and doors close if you don't walk through them. Done when: intro is requested through Cain, a meeting is on the calendar before or at the start of the Fall semester.

**6. Write the YC application — specifically the video**
Why now: The video is what kills most applications, it requires practice, and the Fall window is your strongest narrative moment. Done when: video is recorded, watched back, and sent to 2 people outside Sway for a gut reaction. The Gully's data is your proof. Use it.

**7. Decide the Fall 2026 node list and lock it**
Why now: Scope creep in the first two weeks of semester is how you lose clean data. Done when: the list is written (Gully's + campus gym + one of Foundry/E-Club), each node has a named contact, and you know what you're asking each of them.

**8. Build the Sway Card in-app**
Why now: The Weeks 5–6 recognition launch requires it, and building it under time pressure in the middle of the semester is how it gets done wrong. Done when: a student can open the app after their 3rd check-in and see a card with their regular status, top venue, and session count. Nothing else required for V1.

**9. Draft the privacy one-pager for the Dean conversation**
Why now: FERPA will come up and you want it closed before it opens. Done when: one page, plain language, covers opt-in model, what data is collected, what is never collected (grades, academic records), age verification posture at bar nodes. Have a lawyer review it, even informally.

**10. Ignore everything that isn't on this list**
Payments, NFC hardware, a second campus pitch, a mobile app rewrite, a public launch, press, AI features — none of these move the needle before Fall 2026 semester starts. Done when: you can articulate in one sentence what you are not doing this summer and why.

---

*End of document. Last updated June 2026. Built by the Sway founding team.*

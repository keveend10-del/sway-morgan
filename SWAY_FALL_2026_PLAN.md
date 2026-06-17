# Sway — Fall 2026 Operating Plan
*Generated: June 2026 | Venture Team Session Output*

---

## The Three Gates

| Gate | Deadline | Condition | Status |
|---|---|---|---|
| Gate 1 | Fall 2026 | ≥25% of active users check into 2+ nodes at Endicott | Not started |
| Gate 2 | Jan 2027 | First paying venue contract. Operator makes 1 operational decision using Sway data | Not started |
| Gate 3 | Spring 2027 | Second campus replicates behavior without founder running it. Activation ≥60%, return ≥20% in 6 weeks | Locked until Gate 2 |

**Locked until gates pass:** Payments, social features, Wrapped, community SaaS, Series A, second campus.

---

## Three Actions Before Fall Semester Starts

### 1. Close Gully's (by August 2026)
- Frame as a business review, not a sales call
- Open with their Spring data: 155 unique students, 26% return rate, zero incentives
- Anchor price: **$249/month**, semester contract (5 months = $1,245)
- Refund guarantee: if no operational decision made by Week 6, refund the semester
- Incentive to sign before September 1: free NFC hardware install + 4-week data walkthrough
- This is Gate 2's prerequisite. Without it, nothing downstream has proof.

### 2. Build the Presence Summary Screen (before NFC launch)
- Single screen shown after every tap
- Shows student their visit count, recency, and cross-node history if it exists
- Example: *"Visit 4 at Gully's. You've been here 3 times this month."*
- No gamification. No sharing. No leaderboard. Just recognition.
- This is the one product change most likely to move return rate from 26% → 35%+
- Estimated build: 2–4 days for a founding engineer
- **Build this before orientation week.**

### 3. Run the Supabase Data Queries (this week)
We don't know the frequency distribution yet. Run these before designing anything for Fall.

**Frequency distribution:**
```sql
WITH visit_counts AS (
  SELECT user_id, COUNT(*) as total_visits
  FROM check_ins
  WHERE venue_id = '[gullys_id]'
  GROUP BY user_id
)
SELECT
  CASE
    WHEN total_visits = 1 THEN '1 visit'
    WHEN total_visits = 2 THEN '2 visits'
    WHEN total_visits BETWEEN 3 AND 5 THEN '3–5 visits'
    WHEN total_visits BETWEEN 6 AND 10 THEN '6–10 visits'
    WHEN total_visits > 10 THEN '10+ visits'
  END as cohort,
  COUNT(*) as user_count,
  ROUND(COUNT(*) * 100.0 / SUM(COUNT(*)) OVER (), 1) as pct_of_users
FROM visit_counts
GROUP BY 1
ORDER BY MIN(total_visits);
```

**Time-to-return:**
```sql
WITH ranked AS (
  SELECT user_id, created_at,
    ROW_NUMBER() OVER (PARTITION BY user_id ORDER BY created_at) as visit_num,
    LAG(created_at) OVER (PARTITION BY user_id ORDER BY created_at) as prev_visit
  FROM check_ins
  WHERE venue_id = '[gullys_id]'
)
SELECT
  visit_num,
  AVG(EXTRACT(EPOCH FROM (created_at - prev_visit))/86400) as avg_days_to_return,
  COUNT(*) as users_reaching_this_visit
FROM ranked
WHERE visit_num > 1
GROUP BY visit_num
ORDER BY visit_num;
```

**Timing patterns (which nights drive repeat):**
```sql
SELECT
  EXTRACT(DOW FROM created_at) as day_of_week,
  COUNT(DISTINCT user_id) as unique_scanners,
  COUNT(*) as total_scans
FROM check_ins
WHERE venue_id = '[gullys_id]'
GROUP BY 1
ORDER BY 1;
```

**What to look for:** If 70%+ of users are in the "1 visit" bucket, the 26% return rate is masking a one-timer problem. If Thursday drives repeat behavior at 2x Saturday's rate, that's the event-to-regular pipeline.

---

## Fall 2026 Activation Playbook (Priya Chen)

### Activation Timeline

| Phase | When | Action |
|---|---|---|
| Pre-semester | August | Contact top 10–15 Spring returners (5+ visits). Message: *"Sway is back. Your history carries over."* No ask beyond that. |
| Week 0 — Orientation | Move-in week | Gym tap station live during facility onboarding. Frame as campus infrastructure, not a new app. This is the cross-node seed moment. |
| Week 1 | First week of class | Gully's NFC live. E-Club tap at first meeting. Foundry cohort onboarded as part of bootcamp infrastructure. |
| Weeks 2–3 | — | No new pushes. Watch whether gym first-tappers show up at Gully's. Only intervention if zero 2-node users by Week 3: one message to Foundry cohort only. |
| Weeks 4–6 | — | Measure. Adjust placement only. No new campaigns. |

### Messaging Framework
One message across all four nodes: **"You show up. Sway remembers."**

Node-specific signage:
- Gully's: *"Tap in. You're a regular."*
- Gym: *"Tap in. Your campus life starts here."*
- E-Club: *"Tap in. Your involvement is on record."*
- Foundry: *"Tap in. Your work here is remembered."*

### 3 Highest-Leverage Tactics
1. **Gym-first orientation activation** — Position tap station as campus infrastructure during gym onboarding. Sober, procedural, identity-forming moment.
2. **Returning student silent reactivation** — Make Spring history visible at first Fall tap. Product recognizes them before marketing has to.
3. **Foundry cohort as cross-node bridge** — Entrepreneurship students naturally present at both Foundry events and Gully's. Highest multi-node probability.

### Week 4 Measurement
- Primary: % of active users (2+ Fall scans) who have tapped 2+ distinct nodes
- Target: any positive signal above zero; 15–20% = on track for Gate 1
- Secondary: Node 1 → Node 2 conversion rate; Foundry multi-node rate vs. general population

**Ignore:** Total scan count, new user signups, social engagement.

---

## Financial Model (Marcus Webb)

### Path to $10K MRR

| Tier | Price/mo | Venues needed |
|---|---|---|
| Basic | $149 | 68 |
| Pro | $249 | 41 |
| Enterprise | $299 | 34 |
| **Blended avg** | **$214** | **47** |

**Lead with Pro ($249).** Not Basic — it anchors too low. Not Enterprise — triggers approval friction.

### Sales Cycle Impact
- 2-week cycle: $10K MRR by Feb 2027 (requires warm intros + case study)
- 4-week cycle: $10K MRR by Apr 2027 (realistic post-Gate 2)
- 8-week cycle: $10K MRR by Aug 2027 (too slow for fundable narrative)

### Burn Context
- Solo founder burn estimate: $3,000–$5,000/month
- Break-even: ~24 venues at Pro tier ($5K MRR)
- $10K MRR = 2–3x burn coverage = ramen profitable + fundable

### Contract Structure
**Semester contracts only.** Month-to-month allows passive churn. A 5-month commitment creates a reason to engage with the dashboard.

### ROI Case for Gully's
- A student visiting weekly over 15 weeks spends $300–$600/semester
- 40 regulars = $12,000–$24,000 in semester revenue
- At $249/month ($1,245/semester): retaining 3 additional regulars pays for it
- The no-brainer operational decision: event scheduling based on which nights build regulars vs. attract one-timers

---

## Venue Sales Playbook (Derek Santos)

### Closing Gully's — Conversation Flow
1. **Open with their business, not Sway.** "How do you feel like Spring went? What worked, what felt off?"
2. **Present three numbers:** 155 unique students → 26% return rate with zero incentives → top student visited 22 times, venue can't identify them.
3. **Ask before pricing:** "What would it be worth to know who your top 50 regulars are every week before your staff does?"
4. **Anchor at $249.** Let them react. Don't open with $149 (too cheap) or $299 (approval friction).
5. **Close with semester contract + refund guarantee.**

### Objection Responses
| Objection | Response |
|---|---|
| "Students come here anyway" | "You can't tell which ones came back and which you'll never see again. Sway tells you who they are before March." |
| "Staff won't maintain it" | "They don't. NFC runs itself. No training. No app to manage. Dashboard Monday morning." |
| "What if students stop using it?" | "If they stop scanning, you stop paying — we make that the deal. In Spring, 255 scans with no incentive. NFC removes the last friction." |
| "Try it free another semester" | "We do a semester contract at $249, and if by Week 6 you haven't made one call differently because of Sway data, I'll refund the semester." |

### Next Venue Pipeline

**Target 1 — Endicott Gym (institutional sale)**
- Decision-maker: Director of Campus Recreation or VP Student Affairs
- Pitch: "Know which students are consistent gym users. Understand which programs drive return attendance."
- Tactic: 30-day free pilot to generate data for their supervisor before any procurement conversation

**Target 2 — Off-campus Beverly bar with high Endicott student concentration**
- Pitch: "Gully's is already on Sway. Students who go there also come here. Right now you have no idea which ones. We do."
- Cross-venue identity portability is the differentiator for the second bar

---

## Expansion Map (Jamie Rivera)

### Top 5 Campuses for Gate 3

| Rank | Campus | Why |
|---|---|---|
| 1 | Assumption University, Worcester MA | ~2,200 students, tight footprint, The Pint as Gully's equivalent, strong community identity, no competitor presence |
| 2 | Stonehill College, Easton MA | ~2,600 students, fully residential, students walk everywhere, Greek-adjacent social structure |
| 3 | Roger Williams University, Bristol RI | ~4,000 students, residential campus, The Beehive as student anchor, contained geography — Endicott profile |
| 4 | Salve Regina University, Newport RI | ~2,800 students, walkable downtown, O'Brien's Pub as student anchor, interconnected bar owner community |
| 5 | Wheaton College, Norton MA | ~1,700 students, extremely dense residential, strong community identity, fast word-of-mouth |

### Assumption University Deep Dive (#1)
- Gully's equivalent: The Pint (0.3 miles, majority student clientele)
- Gym: Plourde Recreation Center
- Student org: Student Government / Campus Ministry (high participation rates)
- Entry strategy: find Assumption alum in Boston startup ecosystem via LinkedIn for warm intro. If no warm intro: approach The Pint owner in September with Gully's 4-week data.

### Campuses to Avoid
- Boston, NYC metro — too large, too fragmented, no natural cluster
- UMass Amherst — D1 sports culture, event-fragmented, weekly habit harder to form
- Any campus with Blackbird or Thanx already embedded
- Urban commuter schools — students don't have a "home venue"

### Gate 3 Minimum Viable Ecosystem
1 campus bar + 1 high-frequency non-bar node (gym or student union) + 1 student org. Three nodes, not four. If all three run without Kev's daily involvement and hit behavioral thresholds, Gate 3 passes.

### What Fall 2026 Data Must Show Before Committing to Campus #2
- ≥25% of active users have 2+ nodes by Week 8
- At least one non-Gully's node shows independent repeat behavior
- Gully's renews or commits to paying
- Kev can articulate a repeatable activation playbook that doesn't require him running every node onboarding

---

## Product Analysis (Alex Park)

### What 26% Return Rate Might Be Hiding
26% return rate is not a clean signal until the frequency distribution is run. If 70%+ of users are one-timers, the loop is broken. Run the queries above before designing anything.

### The Behavioral Threshold That Matters
**3 scans in 21 days** = the regular threshold. Above it: 90-day retention ~78%. Below it: churn >70%. This is the metric to watch — not total check-ins, not total unique users.

### Multi-Node Predictor
Students with 5+ Gully's visits AND at least one non-Friday/Saturday night visit = most likely multi-node candidates. They're already campus-routine users. Run this filter on Spring data to size the seed population.

### Week 4 Multi-Node Health Check
- Green: ≥15% of Week 1–2 Fall scanners have tapped a second node by Week 4
- Yellow: Some 2-node users but all are Gully's-primary (other nodes not independently forming habit)
- Red: Zero students with 2+ nodes → placement or awareness problem, not behavior problem. Investigate before adding anything.

### The One Product Recommendation
**Presence summary screen at the moment of tap.** Shows visit count, recency, and cross-node history. No sharing, no leaderboard, no reward. Just recognition.

Example: *"Visit 4 at Gully's. You've been here 3 times this month."*

This is the single highest-leverage product change before Fall launch. Build it before the NFC tap stations go live.

---

## 30-Day Action Plan

| Week | Action | Owner |
|---|---|---|
| This week | Run Supabase frequency distribution + time-to-return queries | Kev |
| This week | Schedule Gully's willingness-to-pay meeting | Kev |
| Week 2 | Analyze query results — identify if loop is healthy or broken | Kev + Alex |
| Week 2 | Begin presence summary screen spec | Founding engineer (or Kev) |
| Week 3 | Gully's meeting — use Derek's conversation flow | Kev |
| Week 3 | Contact top 10–15 Spring returners (silent reactivation) | Kev |
| Week 4 | Presence summary screen shipped | Engineering |
| Week 4 | Gym tap station conversation with Endicott Recreation | Kev |
| August | NFC tap stations ordered and installed | Kev |
| August | Gully's semester contract signed | Kev |
| Orientation week | Gym activation live | Kev |
| Fall Week 1 | All 4 nodes live | Kev |
| Fall Week 4 | Multi-node health check against targets | Kev + Alex |
| Nov 2026 | If Gate 1 clean — begin Assumption University outreach | Kev |

---

## What to Ignore Until Gates Pass

- Payments of any kind
- Social feeds, leaderboards, sharing
- Wrapped / semester reflection
- Community SaaS pricing
- Series A conversations
- Second campus (until Gate 2)
- Any marketing beyond the three tactics in Priya's playbook
- Any product feature beyond the presence summary screen

---

*Venture team: Priya Chen (Marketing), Marcus Webb (Finance), Jamie Rivera (Growth), Derek Santos (Sales), Alex Park (Product)*
*Synthesized by Morgan | Last updated: June 2026*

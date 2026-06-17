# SWAY — VENTURE TEAM ACTIVATION
*Use this document to brief each agent. Each prompt below is self-contained — paste it when invoking the skill.*

---

## HOW TO USE

Each section below is a complete prompt for one team member.
Invoke the skill, then paste the corresponding prompt.

```
/senior-marketing-analyst  → Priya Chen
/financial-analyst         → Marcus Webb
/market-growth-expert      → Jamie Rivera
/venue-sales-specialist    → Derek Santos
/product-growth-analyst    → Alex Park
```

Run them sequentially or in parallel. Each produces one deliverable.
Bring outputs back to Morgan for synthesis.

---

## MASTER CONTEXT BLOCK
*(Included in every prompt below — do not edit)*

```
COMPANY: Sway
WHAT IT IS: Participation infrastructure for real-world communities. NFC/QR check-in creates a verified participation graph — person to venue, person to community, person to event. Every return visit compounds the graph.

ONE LINE: You show up. Sway remembers.

THESIS: The internet knows what you watch, search, and post. It knows almost nothing about where you actually show up, what communities you belong to, what habits persist. Sway captures that gap.

PROVEN SO FAR:
- Spring 2026 pilot at Gully's (on-campus bar, Endicott College, Beverly MA)
- 255 total check-ins, 155 unique users, 81% activation rate, 26% return rate
- 9 weeks, zero incentives, zero discounts, zero staff workflow changes, zero paid marketing
- Most active user: 22 visits in one semester. The venue cannot identify who this person is.

NOT PROVEN YET:
- Whether students use Sway across multiple venues (the multi-node thesis)
- Whether venues will pay for the data
- Whether the behavior transfers to a second campus
- Whether participation history feels personally meaningful to students

CURRENT STAGE: Summer 2026. Pilot paused (students left for summer). No active venues. No revenue.

THREE GATES THAT MUST PASS IN ORDER:
Gate 1 (Fall 2026): The graph compounds — same student identity appears across 4+ nodes at Endicott (Gully's + Gym + Foundry + one club). Target: ≥25% of active users check into 2+ nodes.
Gate 2 (Jan 2027): First paying venue contract. Operator makes at least one operational decision using Sway data.
Gate 3 (Spring 2027): Second campus replicates behavior without founder running it. Activation ≥60%, return ≥20% in 6 weeks.

WHAT IS LOCKED UNTIL GATES PASS:
- Payments (locked until post-Gate 3)
- Circles/social features (locked until Gate 1)
- Wrapped semester reflection (locked until Gate 1)
- Community SaaS pricing (locked until Gate 1)
- Series A (locked until Gate 3)
- Second campus (locked until Gate 2)

FALL 2026 DEPLOYMENT PLAN:
- Gully's re-deploys with NFC tap station (replaces QR)
- Endicott Gym onboards as Node 2
- Foundry (Harvard AI Startup Bootcamp at Endicott) onboards as Node 3
- One student org (Entrepreneurship Club) as Node 4
- Same student identity persists across all nodes

REVENUE MODEL (Phase 1):
- Venue SaaS: $149–$299/month per venue
- No revenue collected to date
- Willingness-to-pay not yet validated

SWAY IS NOT:
- A loyalty app
- A discount platform
- A payments company
- A social media app
- A POS replacement
- A rewards program

FOUNDER: Keveen Delgado. Harvard Foundry cohort, June 2026. Solo founder, seeking founding engineer.

TECH STACK: React, Vite, Tailwind, shadcn/ui, Supabase, React Router, TanStack Query, Framer Motion. Web-first, mobile-feel. QR now, NFC Fall 2026.
```

---

## PRIYA CHEN — Senior Marketing Analyst

**Invoke:** `/senior-marketing-analyst`

**Paste this prompt:**

```
You are Priya Chen, Senior Marketing Analyst. I need a complete student acquisition strategy for Sway's Fall 2026 redeployment at Endicott College.

COMPANY CONTEXT:
[paste Master Context Block above]

YOUR DELIVERABLE:
A student activation playbook for Fall 2026 at Endicott College — specifically designed to get students checking in across 4 nodes (Gully's, Gym, Foundry, E-Club), not just one.

The core problem: in Spring 2026, students scanned at Gully's. We don't know if they'll naturally migrate to scanning at the gym or a club too. The multi-node behavior is the entire thesis.

Answer these questions in your output:
1. What is the single highest-leverage activation moment at the start of Fall semester? (orientation week, first night at Gully's, gym induction, etc.)
2. How do we make the multi-node habit feel natural — not like an app you're being asked to use, but something that happens automatically?
3. What is the messaging to students? (Remember: Sway is NOT a rewards app, NOT a loyalty program. It's participation memory. "You show up. Sway remembers.")
4. How do we activate returning students (who used Sway in Spring) vs. new students differently?
5. What does a low-cost, no-paid-marketing activation look like for a 3,000-student campus?

Constraints:
- Zero paid marketing budget
- No staff should need to explain Sway to students
- No incentives or discounts allowed (corrupts the behavior signal)
- The check-in must remain frictionless — tap and done
- Do not suggest a social feed, leaderboard, or public sharing feature

Output format:
- Activation timeline (pre-semester through week 6)
- Messaging framework for students
- The 3 highest-leverage tactics
- What to measure by week 4 to know if it's working
```

---

## MARCUS WEBB — Financial Analyst

**Invoke:** `/financial-analyst`

**Paste this prompt:**

```
You are Marcus Webb, Financial Analyst. I need a financial model and willingness-to-pay strategy for Sway.

COMPANY CONTEXT:
[paste Master Context Block above]

YOUR DELIVERABLE — TWO PARTS:

PART 1: Willingness-to-Pay Validation Strategy
Sway has never charged a venue. Before Fall 2026, we need to have an honest conversation with Gully's management about whether they'd pay.

Help me:
1. Build the ROI case for a campus bar paying $149–$299/month for participation data. What is the economic value of knowing your top 50 regulars? Of knowing which nights drive repeat visits vs. one-timers?
2. What questions do I ask the operator to surface their willingness-to-pay without anchoring them to a price too early?
3. What would make this a no-brainer vs. a "nice to have"? What's the difference between $149 and $299 in terms of value delivered?
4. What operational decision — if Sway helped them make it — would justify the price immediately?

PART 2: Path to First $10K MRR
Model what it takes to reach $10,000 MRR (first meaningful revenue milestone) using only venue SaaS.

Assumptions to work with:
- Venue SaaS pricing: $149 (basic) / $249 (pro) / $299 (enterprise)
- Target market: campus bars and student-dense venues in the Northeast
- Average sales cycle: unknown — model for 2 weeks, 4 weeks, 8 weeks and show the difference
- Churn risk: high in first semester if value isn't demonstrated

Show:
- Number of venues needed at each price tier to hit $10K MRR
- Which pricing tier to lead with and why
- Burn rate context: what does $10K MRR mean for runway if Kev is solo founder with minimal overhead?
- The Gate 2 milestone (first paying contract) in context of this model

Constraints:
- No payments revenue in this model
- No community SaaS revenue yet
- Conservative: assume 40% of venues pitched convert
```

---

## JAMIE RIVERA — Market Growth Expert

**Invoke:** `/market-growth-expert`

**Paste this prompt:**

```
You are Jamie Rivera, Market Growth Expert. I need a campus expansion sequencing strategy for Sway.

COMPANY CONTEXT:
[paste Master Context Block above]

YOUR DELIVERABLE:
A prioritized expansion map — which campuses to target after Endicott, in what order, and why.

Context on why this matters:
Sway's Gate 3 is proving the model transfers to a second campus without the founder running it. This needs to happen by Spring 2027. The wrong campus choice wastes 4+ months. The right choice proves the playbook is replicable.

What makes a campus ecosystem right for Sway (based on what worked at Endicott):
- Student-dense physical ecosystem — students live, eat, drink, work out, and join clubs all in one area
- At least one campus-adjacent bar or venue with a regular student crowd
- Strong community identity (students feel like they belong to something)
- Accessible founder/operator relationship (we can get in the door)

Answer these questions:
1. Which 5 Northeast campuses are highest-priority targets for Gate 3, ranked and justified?
2. For the top choice: what is the specific campus ecosystem map? (Identify the likely Gully's equivalent, gym, org, and off-campus venue.)
3. What is the outreach strategy to get into a second campus? (Who do we talk to — venue owner? Student life? Campus brand ambassador?)
4. What's the minimum viable ecosystem for Gate 3? (We need multi-node behavior — what's the lowest-lift version that still proves the thesis?)
5. What campuses should we avoid and why?

Focus on Northeast (MA, CT, RI, NH, NY). Consider: urban vs. residential campus dynamic, bar culture, student density, Greek life presence, community cohesion.

Output format:
- Ranked top 5 campuses with 2-3 sentence justification each
- Deep dive on #1 choice: ecosystem map + entry strategy
- What "ready to expand" looks like in Fall 2026 data before committing to campus #2
```

---

## DEREK SANTOS — Venue Sales Specialist

**Invoke:** `/venue-sales-specialist`

**Paste this prompt:**

```
You are Derek Santos, Venue Sales Specialist. I need a complete sales strategy for Sway — both closing Gully's as the first paying customer and building a venue pipeline.

COMPANY CONTEXT:
[paste Master Context Block above]

YOUR DELIVERABLE — TWO PARTS:

PART 1: Closing Gully's
Gully's is the first venue that ran the Sway pilot. They saw the product work. They have real data. But we've never charged them, and we haven't had the money conversation yet.

This summer (by August 2026), we need to have that conversation.

Build me:
1. The exact conversation flow for the willingness-to-pay meeting with Gully's management. What do I open with? How do I present the Spring data compellingly? When do I introduce pricing?
2. The objections I'll face and how to handle each:
   - "Our students just come here anyway, why would I pay for this?"
   - "I'm not sure my staff will maintain it."
   - "What happens if students stop using it?"
   - "Can I try it for free for another semester first?"
3. The anchor: should I open high ($299) and negotiate down, or open at $149 and upsell? What's the right strategy for a single campus bar doing $X in weekly revenue?
4. The close: what does the contract look like? Month-to-month vs. semester vs. annual? What's the incentive to sign before Fall?

PART 2: Next Venue Pipeline
After Gully's, what's the right next venue type to target at Endicott or nearby (Beverly/Salem area)?

Consider:
- Endicott Gym (zero commercial relationship — how do you pitch a campus athletic facility?)
- Off-campus bars in Salem (more foot traffic but less student-dense)
- Coffee shops near campus (low repeat frequency — is this even worth it?)
- Fitness studios in Beverly

For the 2 best next venue targets:
- Give me the outreach email/script
- Give me the value proposition in their language (operators don't care about "participation graphs")
- Give me the objection you'll face and the response

Remember: venues need to hear "I can show you who your regulars are and what brings them back" — not "participation identity infrastructure."
```

---

## ALEX PARK — Product Growth Analyst

**Invoke:** `/product-growth-analyst`

**Paste this prompt:**

```
You are Alex Park, Product Growth Analyst. I need a deep analysis of Sway's Gully's pilot data and a product recommendation for Fall 2026.

COMPANY CONTEXT:
[paste Master Context Block above]

PILOT DATA AVAILABLE:
- 255 total check-ins
- 155 unique users
- 81% activation rate
- 26% return rate (at least one return visit)
- 9-week deployment
- Top user: 22 visits in one semester
- QR-based check-in
- No incentives, no staff prompting, no gamification

We do NOT yet have a full frequency distribution breakdown (1-visit / 2-visit / 3+ / 5+ / 10+ cohorts). That analysis needs to be done.

YOUR DELIVERABLE — THREE PARTS:

PART 1: Pilot Data Analysis Framework
I need to pull the right data from Supabase to understand what actually happened. Build me:
1. The exact analysis I should run on the check-in data to understand return behavior
2. The cohort breakdown that matters: what percentage of users visited 1x / 2x / 3-5x / 6-10x / 10+?
3. The timing patterns: which days/nights drove repeat behavior? Was there a weekly rhythm?
4. The drop-off point: at what visit number do users stop returning? Where does the habit break?
5. The power user profile: what does the top 10% of users look like in terms of frequency, timing, and consistency?

PART 2: Multi-Node Behavior — What to Watch For
Gate 1's entire thesis is that the same student identity will compound across 4 nodes (Gully's + Gym + Foundry + E-Club).

We have never seen this behavior. We don't know if it will happen naturally.

Tell me:
1. What specific user behavior at Gully's in Spring 2026 predicts they'll also check into the gym or a club? (e.g., users who visited 5+ times are more likely to habitualize; users who visited on weekday nights may already be campus-routine users)
2. What does the data need to show by Week 4 of Fall 2026 to confirm multi-node behavior is emerging vs. failing?
3. What is the leading indicator (early signal) that the graph is compounding vs. siloed?

PART 3: Product Recommendation for Fall 2026
Based on Spring 2026 data patterns, what is the one product change most likely to increase:
a) The return rate from 26% to 35%+
b) Multi-node adoption (students scanning at 2+ venues)

Constraints:
- No gamification, no leaderboards, no social feed
- No new features that require staff training
- NFC replaces QR in Fall — assume friction is reduced
- Do not recommend payments, rewards, or discounts

What single product decision — beyond NFC — would most increase the behavior we need to see?
```

---

## SYNTHESIS — BRING BACK TO MORGAN

After running all five agents, return to this workspace and share outputs.

Morgan will synthesize into:
1. Updated FOUNDER_CONTEXT.md (if thesis shifts)
2. Updated SWAY_PATHWAY.md (if gate criteria or timelines shift)
3. A 30-day action plan with owners

---

*Last updated: June 2026*

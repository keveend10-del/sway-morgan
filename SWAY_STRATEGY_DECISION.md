# Sway Strategy Decision Memo
*Internal use — updated June 2026*

---

## 1. Executive Verdict

**Pursue Sway. One disciplined 60-90 day sprint. Prove two things: scan habit forms across multiple nodes, and at least one operator pays because the data is valuable. If neither appears, pivot or stop.**

- Do not drop it. Students checked in without discounts, incentives, or staff prompts. That behavior is real.
- Do not expand blindly. Usage validation is not business validation.
- Do not let this become another semester of deck refinement or feature expansion.
- The decisive question is not whether the story sounds big. It is whether the same students use Sway across multiple places and whether one operator pays to keep seeing it.

| Decision Path | Meaning | Action |
|---|---|---|
| Continue hard | Students use Sway across multiple nodes. At least one operator pays. | Keep building. This is venture-scale participation infrastructure. |
| Pivot | Students like the identity/status layer but venues will not pay. | Pivot toward student/community product. Find another payer. |
| Drop | Students do not care. Usage only happens when pushed. No operator pays after seeing real data. | Stop. |

---

## 2. What Sway Actually Is

Sway is the **Participation OS for real-world communities**.

The core primitive is not a check-in. It is a **session**: a person was physically present in a specific place, during a specific time window, and completed that presence. A session can include person, venue, event, group, arrival time, dwell time, completion status, and cross-venue context.

**Tagline:** You show up. Sway remembers.

Sway is not a loyalty app, rewards platform, POS replacement, payments company, or marketing tool. Those may become layers later. They are not the current business.

The long-term category is the **participation graph**: a record of real-world communities, places, events, and repeated behavior across a person's life.

| Audience | Explanation |
|---|---|
| Student | Sway turns showing up into status. You tap in when you arrive, build regular status, and keep a living record of the places and communities shaping your college life. |
| Venue operator | Sway shows you who your real regulars are, which events bring them back, and whether you're creating repeat behavior — without replacing your POS or changing staff workflow. |
| Investor | Sway is building the participation graph. We start with student-dense ecosystems because repeated physical identity forms fastest there. |
| YC | Foursquare proved people would check in. Blackbird proved venues pay for recognition. Whoop proved repeated behavior can become identity. Sway combines those insights for real-world participation, starting with college ecosystems. |

---

## 3. The Core Mental Model

Sway = Blackbird-style venue recognition + Whoop-style personal identity loop + Foursquare-style presence graph — without becoming a feed-first social network.

| Inspiration | What Sway borrows | What it becomes in Sway |
|---|---|---|
| Blackbird | Venue recognition, regular identification, operator-facing value, eventual commerce | Operators know who comes back, which events create regulars, who deserves recognition |
| Whoop | Repeated behavior becomes personal identity, progress, streaks, status, history | Students feel their Sway profile is a record of their real-world life across places, communities, and events |
| Foursquare | Voluntary presence logging, location graph, check-in habit, status mechanics | A modern participation graph: not just "I went here" but "this is who I am based on where I consistently show up" |

---

## 4. The Honest Pilot Read

**Source of truth numbers — use these everywhere:**

- **255 total check-ins** — Spring 2026, 9-week deployment at Gully's (Endicott College)
- **81% activation rate**
- **26% return rate** (blended)
- Zero paid marketing
- No rewards or incentives
- No staff workflow changes
- QR-based only

**Metric inconsistency — resolve before any external use:**
Other documents in circulation cite 302 check-ins, 191 registered users, 156 active members, 37% return rate, and two different TAM frameworks ($1.2B and $8.16B). These discrepancies need a one-sentence explanation for each or reconciliation to a single number. YC partners will notice this in the first 60 seconds.

**What the pilot proved:**
1. Students scan without incentives.
2. Students create an identity profile voluntarily.
3. Some students return and scan again.
4. Presence can be captured without disrupting venue operations.

**What the pilot did not prove:**
- Venues will pay for this data.
- Behavior transfers across multiple venues.
- Cross-venue density compounds.
- Sway increases venue revenue.
- The scan habit forms independent of social context.

---

## 5. The Jack Steen Problem — Most Important Finding From Re-engagement

Post-pilot re-engagement emails surfaced a critical insight.

When asked whether they kept going to the gym: multiple students said yes. One student (Jack Steen) replied: *"Ya I kept going to gym but never thought to scan."*

**What this means:**

The 26% return rate likely understates actual repeat visit rate. Students returned to the gym. They did not re-scan. The venue habit existed. The scan habit did not transfer.

**Why this matters for the 60-90 day sprint:**

The memo from June 2026 recommends adding 4 new nodes by weeks 3-4. That is premature. Expanding nodes before solving scan habit formation will produce cross-node data that understates actual participation — the same measurement problem at scale.

**Implication for node sequencing:**

- QR scanning at Gully's is a social act at a social entry point. It fits naturally.
- Gym scanning is a solo act in a different behavioral context. Friction is higher.
- Different node types require different check-in mechanisms.
- Passive detection (NFC, Apple Wallet, geofence) becomes critical for non-social nodes.

**The question to answer before expanding nodes:** Why did scan habit form at Gully's but not the gym, and what changes that?

---

## 6. Is This YC-Level?

It can be. The YC-level version is not "venue analytics SaaS for college bars." It is "the identity layer for showing up."

**What YC would like:**
- A weird but plausible insight: digital identity is well understood, but real-world participation is not.
- A simple wedge: tap when you show up.
- A dense initial market: campuses compress repeated behavior, social networks, and geography into one ecosystem.
- A founder-led pilot with real usage and zero-incentive behavior.
- A large possible outcome if the participation graph compounds across nodes and markets.

**What YC would challenge:**
- Is this venture-scale identity infrastructure or just a campus check-in tool?
- Do students care enough about their Sway profile to make this user-owned?
- Will venues pay, or will they only say it is interesting?
- Can this spread across multiple locations in one ecosystem?
- Can the founder stay narrow enough to prove one thing before expanding the story?

**Answer to each:** We don't know yet. That is what the 60-90 day sprint answers.

---

## 7. Gully's Role — Reframed

Gully's is not the best paying customer. It is the best behavior lab.

| Gully's role | Why it matters | Why it is limited |
|---|---|---|
| Behavior lab | Proves students will scan without heavy incentives or staff workflow changes | A small close-knit campus bar may already feel it knows its regulars personally |
| Friendly pilot | Low-friction environment to test QR, repeat behavior, and dashboards | Commercial pain may be weaker because the crowd is familiar |
| Credibility asset | First campus story, real traction numbers, founder-led proof | Cannot alone prove Sway is venture-scale infrastructure |

**The stronger paying customer** is a venue with higher volume, more anonymity, more event variability, and less intuition about who is returning — a larger nightlife venue, a gym, a multi-campus event operator, or a venue serving multiple schools.

| Payer quality | Description |
|---|---|
| Weak early payer | Tiny campus-adjacent bar where the owner personally recognizes the same crowd |
| Better early payer | Student-dense but not student-exclusive venue: larger bar, nightlife spot, event venue, gym |
| Best early payer | Venue actively asking: Which schools drive traffic? Which events bring people back? Who came once vs. who returned? Are we creating regulars or one-night spikes? |

---

## 8. What Sway Becomes — The Fork

| If Sway stays at... | It likely becomes... |
|---|---|
| Single-venue check-in dashboard | A niche analytics tool. Useful but not a large company. |
| Campus bar loyalty/status app | Small campus nightlife product. Hard to scale or monetize. |
| User-owned participation identity across multiple nodes | Potentially venture-scale if identity, status, and operator value compound. |
| Cross-location real-world participation graph | The biggest version: users and operators both care, each node increases value, Sway becomes infrastructure. |

**The make-or-break question:** Can the same person use Sway across 3-5 places in one dense ecosystem, and does that history become something they care about?

---

## 9. The Minimum Viable Graph — Corrected Sequencing

The next milestone is not more check-ins at one venue. It is a minimum viable ecosystem. But **node expansion must follow scan-habit clarity**.

**Sequencing order:**

**Step 1 — Solve scan habit at Gully's first.**
Understand why 74% did not return. Understand why gym users returned physically but did not re-scan. Design the Fall 2026 redeployment around closing this gap (notification timing, re-entry prompts, social mechanics at entry points).

**Step 2 — Add one socially similar node.**
A second venue with a social entry point (another campus bar, event space, or recurring social event) where QR scanning fits naturally. Measure whether the same users carry the scan habit across.

**Step 3 — Add a high-frequency non-social node.**
Campus gym or recreation center. This requires passive detection or a different UX — not just a QR poster. Solve this before assuming gym behavior will produce clean data.

**Step 4 — Add a community/event node.**
Student org, recurring event, or club. Tests community participation and belonging, not just venue attendance.

**Step 5 — Add a larger off-campus venue.**
Tests willingness to pay in a place where the operator does not personally know the crowd.

**Cross-node metrics that matter:**
- How many users check in at 2+ nodes?
- How many users check in at 3+ nodes?
- Does the user profile become more valuable after every check-in?
- Do operators care about student overlap between venues and events?
- Does any operator say "I did not know this before"?

---

## 10. The Demo Should Show the Magic Instantly

The demo does not center on total check-ins. It centers on hidden insight the operator could not have had before.

- Here are the 20 students who came back the most.
- Here are the events that created repeat visitors — and the ones that didn't.
- Here are students who go to both Gully's and the gym.
- Here are people who came once and never returned.
- Here is the cohort that came after one event and returned two weeks later.
- Here is the school breakdown driving your crowd on Thursday nights.

**The magic phrase: "You could not know this before."**

The dashboard must reveal something. If an operator looks at it and thinks "I already knew that," it's not the right insight.

---

## 11. Product Sequence

**Phase 1: Presence** — Who showed up? (QR/NFC, session object, timestamp, venue, user identity)

**Phase 2: Completion** — Was this a real visit? (dwell logic, session expiration, event window, completed participation credit)

**Phase 3: Recognition** — What should this person get for coming back? (regular status, badges, recaps, venue recognition, cross-venue rewards)

**Phase 4: Operator Memory** — What can the venue now know? (repeat visitors, completed promos, event-to-return behavior, group overlap, community participation)

**Phase 5: Session Operations** — How does Sway improve service flow? (table sessions, seat numbers, server context, staff prompts, recognition moments)

**Phase 6: Commerce** — How does money eventually move? (tab management, payments, reservations, stored value)

Payments in Phase 6. Not before. Do not let the roadmap get ahead of Phase 2.

---

## 12. What to Stop Doing Now

- **Stop leading with payments.** Payments are optional in Phase 6, after identity density is proven.
- **Stop leading with post-graduation portable identity.** Interesting. Too speculative for now.
- **Stop pitching door lists, line skip, and operating system language** unless asked. These make the company sound unfocused.
- **Stop adding nodes before solving scan habit.** Cross-node data from users who return but don't scan is misleading signal.
- **Stop relying on market-size math as primary proof.** Fix the metric inconsistency first.
- **Stop treating Gully's willingness to pay as the only commercial test.** It may be too small and too familiar to reveal the real commercial pain.
- **Stop building social features.** No feeds, DMs, stories, or friend requests. Presence, memory, status, recognition — in that order.

---

## 13. The 60-90 Day Validation Sprint

**Core question:** Can Sway become useful across a dense real-world ecosystem, and will any operator pay because the data is valuable?

| Phase | Goal | Key actions |
|---|---|---|
| Weeks 1-2 | Lock thesis, metrics, and operating dashboard | Reconcile all numbers to one source of truth. Fix metric discrepancy. Define one dashboard for pilot data. Surface frequency distribution (2+/3+/5+ cohorts, avg days between sessions). |
| Weeks 3-4 | Understand scan habit gap | Student interviews: why did they not re-scan at the gym? Why did 74% not return to Gully's? What would make scanning feel natural at a non-social venue? Design Fall 2026 re-engagement around answers. |
| Weeks 5-6 | Add first new node | Secure one socially similar venue or event. Track whether existing Gully's users carry the scan habit across. |
| Weeks 7-8 | Drive cross-node usage | Push tap-in habit. Run weekly operator reports. Interview students about profile/status/memory — do they care about their Sway identity? |
| Weeks 9-12 | Force payment decision | Ask Gully's what would make Sway worth $149-$299/month. Ask a larger operator to commit to a paid pilot. Learn why or why not. |

---

## 14. Metrics and Kill Criteria

| Signal | Criteria | Decision |
|---|---|---|
| Strong continue | 500+ check-ins across ecosystem; 250+ unique users; 100+ users with 2+ check-ins; 50+ users across 2+ nodes; one paying venue; students can explain why Sway matters to them | Continue. Consider YC / pre-seed. |
| Medium continue | No paying venue yet, but operator gives specific missing feature and commits to paid pilot after it is solved | Continue narrowly. Fix the gap. Retest. |
| Weak signal | Students check in at one place but cross-node behavior is weak and venues say "cool" without paying | Pivot toward user/community product or change customer segment. |
| Kill signal | Students do not care about identity/status/memory; usage only happens when pushed; no operator pays after seeing real data | Drop or radically rethink. |

---

## 15. Monetization — Keep It Simple

Near-term: flat monthly SaaS for venues. No transaction fees. No POS replacement. No usage-based pricing in Year 1.

| Tier | Price | Value delivered |
|---|---|---|
| Starter | $149/mo | Check-in visibility, repeat visitor identification, peak time data, regular recognition |
| Growth | $249/mo | Event-to-return cohorts, cross-night comparisons, return-rate trends, deeper traffic patterns |
| Pro | $299/mo | Cross-venue identity, regular programs, participation analytics, lightweight messaging later |

**The question to ask operators after showing real data:** "Would you pay $199/month to keep knowing this?"

If no: "What would this need to show you to be worth $199/month?"

Do not anchor on price before showing the demo. Show the magic first. Price second.

---

## 16. Messaging and Positioning

| Use | Line |
|---|---|
| One-sentence category | Sway turns real-world participation into identity. |
| Tagline | You show up. Sway remembers. |
| User line | Sway turns showing up into status. |
| Venue line | Sway helps student-dense venues understand repeat behavior across crowds they cannot personally recognize. |
| Investor line | Sway is building the participation graph — a presence-first identity layer for dense real-world communities. |
| YC line | Foursquare proved people would check in. Blackbird proved venues pay for recognition. Whoop proved repeated behavior can become identity. Sway combines those insights for real-world participation, starting with college ecosystems. |

Do not overshare the roadmap. Pitch presence → identity → recognition → payments later. One layer at a time.

---

## 17. Main Risks

| Risk | Why it matters | How to test |
|---|---|---|
| Venue willingness to pay | Without payment, venue SaaS is not a business | Ask for $149-$299/month after showing real repeat behavior data. Learn why or why not. |
| User identity apathy | Without user-owned identity, Sway is a dashboard, not a network | Test whether students open, share, and care about their profile, status, streaks, and semester recap |
| Scan habit doesn't form | Cross-node data understates real behavior if users return to venues but don't re-scan | Interview non-scanners. Test passive detection at non-social nodes (NFC, Wallet). |
| Single-node trap | One venue does not prove participation infrastructure | Track users across 3-5 nodes before making any infrastructure claims |
| Metric inconsistency | Conflicting numbers destroy trust with investors and partners | One source of truth for every public number, with a one-sentence explanation for any discrepancy |
| Small-bar false negative | Gully's may not pay because the owner already knows the regulars personally | Test commercial pain with a larger, more anonymous, event-variable venue |
| Roadmap drift | Payments, access, messaging, and sponsorships make the story sound scattered | Pitch only presence → identity → recognition. Everything else is later. |

---

## 18. Final Founder Advice

- Do not confuse a big vision with proof. The vision is credible. It must be earned through one dense ecosystem.
- Do not settle for being a check-in dashboard. If students do not care about their Sway identity, the long-term vision is not real yet.
- Do not over-index on Gully's as the payer. Use it to prove behavior. Test a larger venue for commercial pain.
- Do not build a social app. Build presence, memory, status, recognition — and only then social awareness.
- Do not avoid the hard question. Ask for money. If nobody pays after seeing real data, learn fast and pivot.
- Solve the scan habit gap before expanding nodes. Bad data at scale is worse than no data.
- Fix the metric inconsistency before any external conversation. One number, one explanation, every time.

**The next unlock is simple:** The same students use Sway across multiple places. At least one non-obvious operator pays because the data is valuable.

Final verdict: pursue Sway, but with a knife at its throat. One serious 60-90 day sprint. Prove cross-location scan habit and paid operator demand. If those do not appear, pivot hard or stop.

---

*Sway Strategy Decision Memo — Internal use — June 2026*

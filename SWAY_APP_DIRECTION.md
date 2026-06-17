# Sway — App Direction
*Last updated: June 12, 2026*

---

## What We're Building (And Why)

Sway has three concentric layers. Only the core is built. The middle layer — the Native Layer — was designed, documented, and never shipped. Brian Carew's interview confirmed the gap directly.

**Three Layers:**

| Layer | What It Is | Status |
|---|---|---|
| Core | Identity + Presence (tap, verify, count) | Built |
| Native | Recognition, regular status, personal history | **Not built — build this** |
| System | Payments, bookings, discovery | Phase 3+ |

**The gap Carew exposed:** He came 8 times. The app never told him that meant anything. The Native Layer is what makes presence feel like identity.

---

## The Node + Social Graph Arc

Sway is building a physical identity network, not a social network. The distinction:

- Social media measures what you **post**
- Sway measures where you **actually show up**

**Phase 1 (Now):** Identity Infrastructure
- Verify presence, track repeat behavior, help venues understand regulars
- Gully's + Gym = 2 nodes. Same identity across both = start of the graph.

**Phase 2:** Identity + Discovery
- Open Sway and see: "47 people already at Gully's." "Soccer team heading there after practice."
- Not Instagram. Not Snapchat. No content posting. Real-world awareness only.

**Phase 3:** Real-World Social Graph
- Who are the regulars at the same places as me?
- Who goes out on Thursdays?
- Which communities overlap?
- Nobody owns this graph. Instagram owns attention. LinkedIn owns professional identity. Sway owns physical co-presence.

**Order of operations:** Identity → Recognition → Discovery → Social coordination

**Gate 1 (Fall 2026 target):** ≥25% of active users check into 2+ nodes. The graph only becomes valuable when the same identity appears across 4+ nodes at Endicott.

---

## The Carew Problem (Why This Matters Now)

Brian Carew: 8 visits in 21 days. Then stopped.

His exact words:
- "It honestly just faded."
- "It didn't make me feel like more of a regular."
- "The bartenders knew my order — that's what makes someone feel like a regular."

**What this means:** Sway captured his behavior and showed him nothing. The tap produced a number he forgot immediately. The Native Layer is what was missing — a mirror that says *you are a regular*, not just *you scanned*.

His suggestions (drink tracking, leaderboards, skip the line) are wrong answers to the right question. Don't build them. Build the layer that was already designed.

---

## App Roadmap — Locked Sequence

### Pre-App Store — by June 17

| Priority | Build | Why |
|---|---|---|
| 1 | **Presence summary screen at every tap** | Personal stats: visit count, last visit, cross-node history. Mirror, not stage. |
| 2 | **Demote Mug Club winner display** | Personal stats above someone else's win. Keep Mug Club small if at all. |
| 3 | **Empty state → first-tap identity seed** | "You've started your Gully's history. Come back and it grows." Seeds the loop. |
| 4 | **App polish / consistency sweep** | Typography, spacing, button states, loading states. Must be clean for App Store. |
| 5 | **NFC tap flow** | "Welcome back" ≠ "Welcome." Instant confirmation. Frictionless. |

### Pre-Fall — by August

| Priority | Build | Why |
|---|---|---|
| 6 | **Regular status tier (5+ completions)** | "You're a Gully's regular." Completion-earned, not tap-earned. Core Native Layer. |
| 7 | **Personal visit timeline** | Every venue, every visit, in order. Makes 22 visits feel real. |
| 8 | **Cross-node presence tracker** | "You've been to Gully's 8x and the Gym 3x." Gate 1 proof requires this to be visible. |
| 9 | **Returning student history on first open** | Spring users see their history immediately. Re-activation hook, zero spend. |
| 10 | **Sway Recap / Semester Wrapped** | End of Fall. Makes the identity layer feel earned. Full semester in one view. |

---

## Completion Philosophy (Non-Negotiable)

From the Completion/Points doc — these rules protect the thesis:

- **Tap ≠ reward.** Intent is not credit.
- **Completion = credit.** A completed session earns status. Not a scan.
- **Points are presence, not currency.** Never map to spend. Never behave like money.
- **Rewards are recognition artifacts.** A "regular" status, a tier, a symbolic perk. Not a discount.
- **If it requires policing, the design is wrong.** System should be naturally resistant to gaming.

**Why this matters for GPS check-in (Carew's suggestion):** Passive location detection = passive presence = unverified session. The Completion thesis requires intentional presence. GPS auto-checkin corrupts the behavioral signal. Do not build it.

---

## Do Not Build (Confirmed)

| Feature | Why Not |
|---|---|
| GPS auto check-in | Passive presence ≠ verified identity. Corrupts completion thesis. |
| Drink tracking / leaderboards | Untappd already exists. Alcohol liability. Thesis violation. |
| Skip-the-line incentives | Discount-adjacent. Corrupts behavior signal. |
| Social feed / DMs / friend requests | Phase 2+. Hundreds of startups die here. |
| Payments | Phase 3. Locked until Gate 2 passed. |
| Blockchain / crypto | Not part of the product. |
| POS replacement | Not the play. Runs alongside POS. |

---

## Venue Dashboard — Same Feature, Two Faces

Regular status on the student side = venue dashboard ROI on the operator side.

When a student earns "Regular" status at Gully's (5+ completions), the venue dashboard surfaces them as a confirmed regular. The venue can now make an operational decision about that person.

**This is what the venue is paying for:** a ranked list of proven regulars, updated every semester, built from behavioral completion data — not survey responses, not spend data, not loyalty points.

Pitch: *"Sway tells you who your regulars are before they feel like one."*

---

## What "Sway Is" — 3-Layer Explanation

**To a student:**
"Sway tracks where you show up and builds your regular status. You tap in when you arrive, build streaks, earn recognition, and compete for Mug Club."

**To a venue operator:**
"Sway shows you who your real regulars are and helps increase repeat visits through visible recognition and cross-venue identity. Runs alongside your POS — no replacement needed."

**To an investor:**
"Sway is the identity layer for physical commerce. We verify presence, increase repeat behavior through recognition, and over time become the control layer above POS systems."

**One sentence:**
"Sway turns showing up into status."

---

## One-Line Filters

Before building anything:
1. Does this increase identity density or repeat visibility?
2. Does it reduce venue friction or improve operator insight?
3. Does it preserve staff simplicity?
4. Does it avoid payment-first confusion?
5. Does it produce measurable signal?

If most answers are no → don't build it.

---

*Reference: Session 005 (June 11–12, 2026). Carew interview, Docs review, Agent synthesis.*

# Sway Legal Hygiene Sprint — Summer 2026

**Initiated:** 2026-06-19  
**Status:** Day 1 complete. Days 2–7 pending.  
**Google Drive folder:** Sway Legal Hygiene — Summer 2026

---

## The One-Line Frame

Clean up legal foundation so nothing messy blocks investors later — while keeping the summer sprint focused on proving the mechanism (recognition system, 3–5 venue cluster, lift metrics). Legal work supports the sprint; it does not distract from it.

---

## Google Drive Folder Structure (created 2026-06-19)

```
Sway Legal Hygiene — Summer 2026/
├── Company Formation/
├── IP & Contributors/
│   └── Sway Contributor & IP Tracker (Google Sheet) ✅
├── Venue Agreements/
├── Privacy & Terms/
├── Pilot Metrics & Proof/
│   └── Gully's Proof Summary — Spring 2026 ✅
├── Advisor Agreements/
└── Future Payments — Not Active/

Sway Product Scope & Legal Positioning Memo (root) ✅
```

---

## 7-Day Sprint Plan

### Day 1 — COMPLETE ✅
- [x] Create Google Drive folder structure (7 subfolders)
- [x] Create Sway Product Scope & Legal Positioning Memo
- [x] Create Sway Contributor & IP Tracker (Google Sheet — fill in real names)
- [x] Create Gully's Proof Summary — Spring 2026 (Gully's-only numbers)
- [x] Create lawyer outreach Gmail draft (id: r-6908312013270331100)

**Open before Day 2:** Confirm Gully's unique user count (67 or 69?) via Supabase SQL, excluding test accounts.

---

### Day 2
- [ ] Finalize Gully's Proof Summary — confirm user count, add Supabase query results
- [ ] Fill in all real names in Sway Contributor & IP Tracker
  - Engineer candidate (URGENT — no agreement in place)
  - Designer (if any)
  - Any branding contributors
  - Advisors giving repeated strategic input

---

### Day 3
- [ ] Draft Sway Venue Pilot Agreement — v0.1 (save to Venue Agreements folder)

Cover:
- Venue gives permission to operate Sway on premises
- Sway can place QR/NFC check-in materials
- Users opt in voluntarily
- Venue gets dashboard access
- No POS replacement
- No payment processing
- No alcohol-consumption rewards
- No staff workflow change required
- Pilot length: 60–90 days
- Pilot fee: $99/month (validation phase)
- Sway can use anonymized/aggregated metrics in investor materials
- Either side can stop with notice

- [ ] Prepare Gully's Fall continuation ask + Village paid pilot ask (use this agreement as basis)

---

### Day 4
- [ ] Create Sway Data Map — v0.1 (save to Privacy & Terms folder)

Columns: Data collected | Why collected | Who sees it | Retention | User control | Risk

Data to map:
- Name
- Email
- Venue check-in
- Timestamp
- Event check-in
- Repeat visit count
- Venue-specific status
- Future GPS prompt status (if added)
- Future Apple Wallet/pass status (if added)

- [ ] Draft plain-English consent statement:
  - Sway does not sell student location data
  - Sway does not publicly broadcast exact location by default
  - Sway uses check-ins to create participation history and venue-level insights
  - Users should understand what is being recorded before participating

---

### Day 5
- [ ] Email 2–3 startup lawyers (use Gmail draft r-6908312013270331100 as template)
  - David Ferguson referral (via Gina / Foundry)
  - Brian SCORE referral
  - One additional if available
- [ ] Ask: 30-minute startup formation/legal hygiene consult — not full legal services

---

### Day 6
- [ ] Build advisor bench list (save to Advisor Agreements folder)
  - 2–4 people max
  - No formal board, no SAB
  - For each: name, domain, what they bring, comp structure (equity vs. advisory)

---

### Day 7 — Package
- [ ] Create "Sway Summer Validation Packet" folder or doc containing:
  - Product Scope Memo ✅
  - Gully's Proof Summary ✅
  - Venue Pilot Agreement outline (Day 3)
  - Data Map (Day 4)
  - IP Tracker (Day 1, filled in)
  - Advisor Bench (Day 6)
  - Fall 3–5 Node Plan (pull from FOUNDER_CONTEXT + SWAY_STRATEGY_DECISION)

---

## What NOT To Do (do not drift into these)

- Formal board structure
- Scientific Advisory Board (SAB)
- SOC 2
- Patents (unless counsel flags something truly protectable)
- Token / ownership / stablecoin docs
- Payment routing or sponsor bank docs
- Employment handbook
- Complex investor financing documents
- Long-term governance

---

## Lawyer Outreach Email Template

Subject: Startup Legal Guidance — Sway (Participation Platform, Early Pilot Stage)

> Hi [Name],
>
> I'm the founder of Sway, a student-venue participation platform currently live at Gully's, the on-campus bar at Endicott College in Beverly, MA. We completed our first pilot this spring and are preparing for Fall 2026 redeployment.
>
> I'm looking for lightweight startup legal guidance — not a large legal project yet.
>
> The main areas I want to clean up: entity formation (LLC → C-Corp timing), founder/IP assignment, contractor and advisor agreements, privacy/terms basics, and a simple venue pilot agreement for paid validation pilots.
>
> Sway is not currently processing payments, storing value, or replacing POS systems. It is a QR/NFC-style check-in and venue analytics layer focused on repeat behavior and participation identity.
>
> Would you be open to a short intro call to see if this is a fit?
>
> Best,  
> Keveen Delgado  
> Founder, Sway

---

## Key Reminder

"Your job right now is not to look like a mature company. Your job is to look like a serious early founder: 'I'm proving the participation graph at Endicott. Gully's is live. The next milestone is paid venue validation and multi-node density. I'm cleaning up legal basics now so IP, privacy, and pilot agreements don't become problems later.'"

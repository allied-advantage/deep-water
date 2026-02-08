# Opportunity Log — Scored & Ranked

> Running list of opportunities, scored by the Engine's rubric.
> Updated by Research Loop. Highest-scoring validated opportunity becomes ACTIVE_OPPORTUNITY.

---

## Scoring Rubric (v2)

Every opportunity scored **1–10** on five dimensions:

| Dimension | Weight | 1-3 | 4-6 | 7-10 |
|-----------|--------|-----|-----|------|
| **Novelty** | 20% | Everyone does this | Some do this | No one does this |
| **TAM** | 20% | <$10M tiny niche | $50-500M mid-market | $500M+ large market |
| **Build Complexity** | 20% | 6+ months, complex | 2-4 weeks, moderate | Weekend to 1 week, simple |
| **Time-to-Revenue** | 20% | 1+ year runway needed | 3-6 months realistic | <30 days to first dollar |
| **Moat Potential** | 20% | None, easy to copy | Mild (expertise, niche) | Strong (data, network, regulation) |

### Composite Score Formula

```
Score = (Novelty × 0.2) + (TAM × 0.2) + (BuildEase × 0.2) + (TimeRev × 0.2) + (Moat × 0.2)
```

### Score Ranges
- **7.5–10.0** → 🔴 **BUILD NOW.** Transition to Build Loop.
- **6.0–7.4** → 🟡 **Strong candidate.** Validate further or keep in queue.
- **4.0–5.9** → 🔵 **Interesting.** Watch for changes.
- **1.0–3.9** → ⚪ **Pass.** Archive.

### Strategic Filters (Must Pass)
- ✅ **Phase 3** (Vertical application, not infrastructure)
- ✅ **Use 🚂** (Using the railroad, not building it)
- ✅ **Aligned** (Matches Austin's skills: RE, sales, AI automation, ads)

---

## Active Opportunities

| Date | Opportunity | Nov | TAM | Build | T2R | Moat | **Score** | Status |
|------|------------|-----|-----|-------|-----|------|-----------|--------|
| 2026-02-07 | **State AI Compliance Navigator for SMBs** — Self-serve tool for 50-state AI law compliance. Track which states your customers are in, what AI you use, generate required disclosures, bias audit templates, documentation. Key deadlines: IL Jan 2026, CO Feb 2026, VA Jan 2026. 69% of SMBs overspend on compliance vs large competitors. Vanta/Drata focus on SOC 2/HIPAA, not state AI laws. | 7 | 7 | 5 | 7 | 6 | **6.4** | 🟡 explore |
| 2026-02-07 | **ADA Title II Accessibility for Municipalities** — Audit + remediation for 90k local gov websites. WCAG 2.1 AA deadline April 24, 2026. Most small municipalities unprepared. Accessibility exists but municipal focus undersold. | 6 | 8 | 6 | 8 | 5 | **6.6** | 🟡 explore |
| 2026-02-07 | **SEC Reg S-P Compliance for Small RIAs** — Turnkey incident response + breach notification for small financial advisors. June 3, 2026 deadline. ~15k small RIAs lack compliance staff. | 6 | 7 | 5 | 8 | 5 | **6.2** | 🟡 explore |
| 2026-02-07 | **Colorado AI Act Compliance for SMBs** — Self-serve tool for SB 205 compliance. Impact assessments, risk mgmt templates, disclosures. Enforcement June 30, 2026. Enterprise has TrustArc/OneTrust; SMB gap exists but moat weak. | 7 | 6 | 5 | 8 | 4 | **6.0** | 🟡 explore |
| 2026-02-07 | **Agency Client Onboarding Automation** — Portal + automated checklists + doc collection. Reddit shows 4hr onboarding time per client; could reduce to 30 min. Agencies are high-volume onboarders with clear pain. n8n + typeform + GHL stack. | 7 | 7 | 8 | 8 | 6 | **7.2** | 🟡 explore |
| 2026-02-07 | **SMB Contract/Renewal Alert System** — Upload contracts → OCR extracts dates → alerts at 30/60/90 days. Enterprise has Ironclad/Summize; SMBs track in spreadsheets. Simple SaaS, clear pain from Reddit. | 7 | 6 | 9 | 8 | 5 | **7.0** | 🟡 explore |
| 2026-02-07 | **PPC/Marketing Report Automation for Agencies** — Auto-pull from GA4/Meta/Google Ads, generate PDF reports. Reddit: "5-6 hours per large client monthly." Tools exist (Looker Studio, Hurree) but fragmented. | 5 | 7 | 7 | 8 | 4 | **6.2** | 🟡 explore |
| 2026-02-07 | **Employee Onboarding Workflow Automation** — Reddit: "80 separate things per hire, all time-sensitive." IT + HR checklist automation with status tracking. Adaxes exists for IT-heavy; gap for small/mid orgs. | 5 | 7 | 6 | 7 | 4 | **5.8** | 🔵 watch |
| 2026-02-06 | **Quote/Estimate Follow-Up Voice AI** — Outbound voice calls 24-48h after estimate to handle objections, answer questions, book jobs. Home services conversion gap: 40-50% (low) vs 70-80% (high). Even 5% lift = significant ROI. Could be aiservicecalls feature tier. | 7 | 7 | 8 | 9 | 5 | **7.2** | 🟡 explore |
| 2026-02-06 | **Seasonal Reminder Voice AI** — Outbound voice calls for seasonal services (Spring AC, Fall heating, etc). Text reminders exist; voice calls get higher engagement. Cross-sell opportunity. Uses existing VAPI stack. | 7 | 7 | 8 | 8 | 5 | **7.0** | 🟡 explore |
| 2026-02-06 | **Win-Back/Reactivation Voice AI** — Outbound calls to customers who haven't booked in 6+ months. Most reactivation campaigns are email/text; voice is underserved. Clear ROI if even 5% reactivate. | 7 | 6 | 8 | 8 | 5 | **6.8** | 🟡 explore |
| 2026-02-06 | **Voice AI Review Solicitation + Service Recovery** — Outbound calls after service to thank customers, quick NPS check, guide happy customers to Google reviews, escalate unhappy ones to human before bad review. Higher response than text/email. Uses existing VAPI stack. | 7 | 7 | 8 | 8 | 5 | **7.0** | 🟡 explore |
| 2026-02-06 | **AR Collection Voice AI for SMBs** — Outbound voice calls for past-due invoice reminders. SMBs can't afford human collectors. Clear ROI: get paid faster. Integrate with QuickBooks/Stripe. | 6 | 7 | 7 | 8 | 5 | **6.6** | 🟡 explore |
| 2026-02-06 | **Property Management Emergency Dispatch** — Voice AI for after-hours emergency calls. Triage, dispatch from approved contractor list, replace $150-300/mo answering services. Cross-sell with Deep Water contractor network. | 5 | 6 | 8 | 8 | 5 | **6.4** | 🟡 explore |
| 2026-02-06 | **Trade Contractor License/CE Tracker** — Simple deadline reminder service for trade licenses (HVAC, plumbing, electrical). Healthcare tools exist; blue-collar underserved. | 6 | 6 | 8 | 6 | 4 | **6.0** | 🟡 explore |
| 2026-02-05 | **"SaaSpocalypse Response" Content/Positioning** — SMBs asking "can AI do this?" Position Allied Advantage as the answer. Time-sensitive news cycle. | 5 | 7 | 10 | 10 | 4 | **7.2** | 🟡 validate |
| 2026-02-04 | **Fractional FTE Pricing Model** — Price AI services as "0.5 FTE replacement" not retainers. Makes ROI trivially calculable. | 6 | 7 | 10 | 9 | 5 | **7.4** | 🟡 validate |
| 2026-02-04 | **"AI MAX Expert" for RE PPC** — Position as THE experts making Google AI MAX work. 84% fail due to poor setup. | 6 | 6 | 9 | 8 | 6 | **7.0** | 🟡 validate |
| 2026-02-01 | **Voice AI Vertical Playbooks** — Productize VAPI+n8n+GHL stack for specific verticals. RE wholesaling first. | 6 | 6 | 8 | 7 | 6 | **6.6** | 🟡 explore |
| 2026-02-01 | **AI Review Response for Blue-Collar SMBs** — $20-50/mo review responder. Unbundles Podium/Birdeye. | 5 | 6 | 9 | 8 | 4 | **6.4** | 🟡 explore |
| 2026-01-31 | **Agent-First CRM for RE Wholesalers** — CRM built around AI agents. Auto-qualify, auto-follow-up. | 6 | 5 | 5 | 5 | 6 | **5.4** | 🔵 watch |
| 2026-01-31 | **TX OSSF/Septic Compliance SaaS** — Regulatory mandate, manual county processes. From Nightwatch. | 7 | 4 | 6 | 6 | 8 | **6.2** | 🟡 validate |
| 2026-01-31 | **AI Implementation Agency Positioning** — Expand Allied beyond ads to full AI ops implementation. | 5 | 7 | 9 | 7 | 5 | **6.6** | 🟡 explore |
| 2026-02-01 | **Agentic Ad Campaign Management** — Agent-managed Google/Meta Ads as premium tier. | 5 | 7 | 5 | 6 | 5 | **5.6** | 🔵 watch |

### Column Key
- **Nov** = Novelty (1-10)
- **TAM** = Market Size (1-10)
- **Build** = Build Complexity inverted (10 = easy, 1 = hard)
- **T2R** = Time-to-Revenue inverted (10 = fast, 1 = slow)
- **Moat** = Moat Potential (1-10)
- **Status**: `explore` → `validate` → `🔴 build` → `live` | `watch` | `passed`

---

## Archived / Passed

| Date | Opportunity | Score | Reason |
|------|------------|-------|--------|
| 2026-01-31 | Voice agents for contractors | — | Already building (Deep Water) |
| 2026-01-31 | Elder care coordination | 4.2 | No conviction after research |
| 2026-01-31 | QuickBooks alternatives | 3.5 | Too competitive |
| 2026-01-31 | Pool service software | 3.8 | Well-funded incumbents (Skimmer $74M) |
| 2026-01-31 | Consumer apps generally | — | Low ARPU, hard acquisition |
| 2026-01-31 | Marketplaces | — | Chicken-and-egg problem |

---

## How Research Loop Adds Opportunities

1. **Discover** potential opportunity through research
2. **Score** each dimension 1-10 honestly
3. **Apply filters**: Must be Phase 3, Use 🚂, Aligned
4. **Calculate** composite score
5. **Validate** if score ≥ 6.0 (test with real data/outreach)
6. **If score ≥ 8.0 AND validated**: Write to ACTIVE_OPPORTUNITY.md, transition state

---

## Queue Rules

1. Only ONE opportunity in ACTIVE_OPPORTUNITY.md at a time
2. If current opportunity fails in Build phase → return to queue, pick next highest
3. After launch → opportunity moves to "live", Research Loop continues finding next
4. Research never stops, even during Build/GTM phases

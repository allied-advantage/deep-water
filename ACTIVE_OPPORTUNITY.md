# Active Opportunity: AI Service Calls (Deep Water)

## Summary
AI-powered phone answering service for home service contractors. When a customer calls, our AI answers, qualifies the lead, books appointments, and sends details to the contractor's CRM. Contractors pay per qualified booked call — only pay for results.

## Scores
| Dimension | Score | Notes |
|-----------|-------|-------|
| Novelty | 7/10 | Outcome-based pricing is differentiated; AI answering exists but not common for SMB contractors |
| TAM | 9/10 | 500K+ home service contractors in US alone, $50B+ market |
| Build Complexity | 8/10 | MVP already 80% built (VAPI + n8n + GHL) |
| Time-to-Revenue | 9/10 | Can onboard first contractor this week |
| Moat Potential | 6/10 | Execution speed + vertical focus; tech is replicable |
| **TOTAL** | **7.8/10** | |

## Validation Evidence
- Contractors constantly miss calls (30-60% go to voicemail)
- Missed calls = lost revenue ($500+ per job)
- Existing solutions charge $200-400/mo flat fee with no guarantee
- Austin has direct access to contractor networks via RE investing

## Target Customer
- **Who:** Home service contractors (HVAC, plumbing, electrical, roofing)
- **Pain:** Missing customer calls, losing jobs to competitors who answer first
- **Current Solution:** Voicemail, call centers ($300+/mo), or nothing
- **Willingness to Pay:** Proven — they already pay for answering services

## MVP Scope
- [x] VAPI assistant configuration
- [x] n8n call processing workflow
- [x] SMS/Email notifications
- [x] Google Sheets logging
- [x] Provisioning script
- [x] **Onboarding form** (HTML form on landing page + n8n workflow)
- [ ] **Connect onboarding to provisioning automation** (import workflow to n8n)
- [ ] **End-to-end contractor signup test**
- [ ] **First beta contractor account**

## Tech Stack
- Landing: aiservicecalls.com (Cloudflare)
- Voice AI: VAPI
- Automation: n8n
- CRM: GoHighLevel
- Database: Supabase

## Success Criteria
- Contractor can sign up self-serve
- Calls route to AI, get qualified, booked
- Contractor receives lead in their CRM
- Billing tracks qualified calls

## Risks
- **Call quality:** Mitigate with extensive testing + human fallback
- **Contractor adoption:** Start with warm network (Austin's RE contacts)
- **Competition:** Move fast, lock in early customers

---

## Current Phase: **BUILDING**

Next tasks:
1. ~~Create onboarding form~~ ✅ Done — form exists + n8n workflow created
2. Import n8n workflow + configure credentials
3. Test full signup flow end-to-end
4. Onboard first beta contractor

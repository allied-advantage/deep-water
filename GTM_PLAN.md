# GTM Plan

> Maintained by GTM Loop. Full launch package created here.

---

## Template

When GTM Loop is active, this file will contain:

```markdown
# GTM Plan: {Opportunity Name}

## Launch Checklist

- [ ] Google Ads campaign ready
- [ ] Meta Ads campaign ready
- [ ] Email sequence in Instantly
- [ ] Call script finalized
- [ ] Lead list generated
- [ ] Landing page live and tested
- [ ] Tracking pixels installed
- [ ] Austin final review

---

## Google Ads

### Keywords
| Keyword | Match Type | Est. CPC | Intent |
|---------|------------|----------|--------|
| {keyword 1} | Exact | $X.XX | High |
| {keyword 2} | Phrase | $X.XX | Medium |

### Ad Copy

**Headline 1:** {30 chars}
**Headline 2:** {30 chars}
**Headline 3:** {30 chars}
**Description 1:** {90 chars}
**Description 2:** {90 chars}

### Campaign Structure
- Campaign: {Name}
- Ad Groups: {List}
- Daily Budget: ${X}
- Bid Strategy: {Maximize conversions / Target CPA}

---

## Meta Ads

### Audiences
1. **Custom Audience:** {Description}
2. **Lookalike:** {Based on X}
3. **Interest-based:** {Interests}

### Ad Creative Concepts
1. **Hook:** {Attention grabber}
   **Body:** {Value prop}
   **CTA:** {Action}

2. **Hook:** {Alternative angle}
   **Body:** {Different benefit}
   **CTA:** {Action}

### Campaign Structure
- Objective: {Lead gen / Conversions}
- Placements: {Feed, Stories, etc.}
- Daily Budget: ${X}

---

## Email Sequence (Instantly)

### Email 1: Introduction
**Subject:** {Subject line}
**Body:**
```
Hi {{firstName}},

{Body copy with {{companyName}} variable}

{CTA}
```
**Send:** Day 1

### Email 2: Value Add
**Subject:** {Subject line}
**Body:** {Copy}
**Send:** Day 3

### Email 3: Case Study
**Subject:** {Subject line}
**Body:** {Copy}
**Send:** Day 6

### Email 4: Final
**Subject:** {Subject line}
**Body:** {Copy}
**Send:** Day 10

---

## Call Script

### Opener
"{Script}"

### Qualify
- {Question 1}
- {Question 2}
- {Question 3}

### Pitch
"{Value prop delivery}"

### Objection Handling
- **"Too expensive":** {Response}
- **"We already have X":** {Response}
- **"Not interested":** {Response}

### Close
"{CTA and next steps}"

---

## Lead List

**Criteria:**
- Industry: {X}
- Company Size: {X employees}
- Location: {X}
- Titles: {X, Y, Z}

**Source:** {Apollo / LinkedIn / Manual}

**File:** `builds/{opportunity}/leads/initial-list.csv`

**Columns:** firstName, lastName, email, companyName, phone, title
```

---

## Current Status

No active GTM preparation. Waiting for Austin to approve MVP.

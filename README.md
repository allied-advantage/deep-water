# Opportunity Engine

**Autonomous opportunity discovery, validation, building, and go-to-market.**

## What Is This

Three autonomous loops running on cron:

1. **Research Loop** (every 4h) — Scans for opportunities, validates, scores
2. **Build Loop** (every 2h) — Builds MVP when opportunity found
3. **GTM Loop** (every 4h) — Creates launch package when MVP approved

Austin's role: Approve transitions, provide feedback, close deals.

---

## Quick Status

```bash
# Check current state
cat projects/opportunity-engine/STATE.json
```

| Phase | What's Happening |
|-------|------------------|
| `research` | Scanning for opportunities |
| `building` | Building MVP for current opportunity |
| `review` | MVP done, awaiting Austin approval |
| `gtm-prep` | Creating ads, emails, call scripts |
| `gtm-review` | GTM ready, awaiting Austin approval |
| `live` | Launched! (Research continues in parallel) |

---

## How Austin Interacts

### Via Telegram Commands

| Command | What It Does |
|---------|--------------|
| `approve mvp` | Transitions from `review` → `gtm-prep` |
| `approve gtm` or `launch` | Transitions from `gtm-review` → `live` |
| `pause` | Stops all loops (sets `token_budget_paused: true`) |
| `resume` | Restarts loops |
| `status` | Reports current state and activity |
| `focus on {topic}` | Adds constraint to research focus |

### Notifications You'll Receive

- **Opportunity found:** "Found 8+/10 opportunity: {name}. Starting build."
- **MVP ready:** "MVP complete for {name}. Demo: {url}. Reply 'approve mvp' to proceed."
- **GTM ready:** "GTM package ready. Reply 'approve gtm' to launch."
- **Budget pause:** "Hit 25% token budget. Pausing until tomorrow."

---

## File Structure

```
projects/opportunity-engine/
├── MISSION.md              # Why we're doing this
├── ARCHITECTURE.md         # How the system works
├── README.md               # You are here
├── STATE.json              # Current machine state
├── SCRATCHPAD.md           # Research memory (learnings, hypotheses)
├── OPPORTUNITIES.md        # Ranked opportunity list
├── ACTIVE_OPPORTUNITY.md   # Currently building (if any)
├── BUILD_LOG.md            # Build phase decisions/blockers
├── BUILD_PLAN.md           # Current build plan
├── GTM_PLAN.md             # Launch package (ads, emails, scripts)
└── builds/                 # Code for each opportunity
    └── {opportunity-name}/
```

---

## How to Pause/Resume

**Pause everything:**
- Say "pause" on Telegram, OR
- Edit STATE.json: `"token_budget_paused": true`

**Resume:**
- Say "resume" on Telegram, OR
- Edit STATE.json: `"token_budget_paused": false`

---

## How to Add Focus Areas

Two ways:

1. **Telegram:** "Focus on {topic}" — adds to SCRATCHPAD.md
2. **Direct edit:** Add to SCRATCHPAD.md under "Promising Threads"

Research Loop reads SCRATCHPAD.md and weights these areas higher.

---

## How to Skip an Opportunity

If you don't like the current opportunity:

1. Edit STATE.json: Set `"phase": "research"`
2. Move opportunity to "Archived" in OPPORTUNITIES.md
3. Delete or clear ACTIVE_OPPORTUNITY.md

Research Loop will find the next one.

---

## Budget Controls

- Loops pause at **25% daily token usage**
- Max **5 research iterations** before human checkpoint
- All state checkpointed — safe to kill and resume

---

## What Gets Built

### Landing Pages
- HTML/Tailwind or Next.js
- Hosted on Vercel or Cloudflare Pages
- Mobile-responsive
- Clear CTA

### Core Software (as needed)
- Supabase for database
- n8n for workflows
- VAPI for voice AI
- GHL for CRM/automation

### GTM Package
- Google Ads: Keywords, ad copy, campaign structure
- Meta Ads: Audiences, creative concepts
- Email: 3-4 sequence for Instantly ({{firstName}}, {{companyName}} variables)
- Calls: Script + lead list CSV for GHL

---

## Troubleshooting

### "Loop isn't running"
1. Check STATE.json — is `token_budget_paused: true`?
2. Check cron job status
3. Check if phase allows that loop (Build only runs when `phase: building`)

### "Stuck in review"
- MVP is done, waiting for your "approve mvp" command

### "Want to start fresh"
1. Reset STATE.json to initial state
2. Clear ACTIVE_OPPORTUNITY.md
3. Optionally archive current opportunities

---

## Architecture Deep Dive

See [ARCHITECTURE.md](ARCHITECTURE.md) for:
- Full loop diagrams
- Scoring criteria details
- State machine transitions
- Phase-by-phase breakdown

See [MISSION.md](MISSION.md) for:
- Strategic filters
- What we're hunting (and not hunting)
- Success metrics

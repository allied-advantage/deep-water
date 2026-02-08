# Opportunity Engine v2 Architecture

## Overview

A fully autonomous business discovery and execution machine. Four stages, human approval gates, parallel execution where possible.

```
┌─────────────────────────────────────────────────────────────────────┐
│                        OPPORTUNITY ENGINE v2                        │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│   ┌─────────────┐                                                   │
│   │  RESEARCH   │  ← 4h cron, Ralph Wiggum loops internally        │
│   │   Agent     │    Spawns collectors, synthesizes, scores        │
│   └──────┬──────┘                                                   │
│          │                                                          │
│          ▼ [notify Austin, await approval]                          │
│                                                                     │
│   ┌─────────────┐                                                   │
│   │  PRODUCT    │  ← Triggered by approval                         │
│   │   Agent     │    Defines spec, monetization, GTM strategy      │
│   └──────┬──────┘                                                   │
│          │                                                          │
│          ▼ [notify Austin, await approval]                          │
│                                                                     │
│   ┌─────────────┬─────────────┐                                     │
│   │   BUILD     │    GTM      │  ← Parallel 15min crons            │
│   │   Agent     │   Agent     │    Check JOB_BOARD.json            │
│   └──────┬──────┴──────┬──────┘                                     │
│          │             │                                            │
│          ▼             ▼                                            │
│   [notify when both complete]                                       │
│                                                                     │
│   ┌─────────────┐                                                   │
│   │   LAUNCH    │  ← Human triggers final go-live                  │
│   └─────────────┘                                                   │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

## Stages

### 1. RESEARCH (Every 4 hours)

**Goal:** Find novel, non-obvious money-making opportunities

**Process:**
1. Spawn 3 data collectors (Sonnet model):
   - Collector 1: Unsexy B2B pain points (compliance, ops, boring industries)
   - Collector 2: Regulatory/info asymmetry opportunities
   - Collector 3: AI automation gaps in traditional industries

2. Synthesize findings (Opus model):
   - Pattern recognition across collector outputs
   - Novelty assessment
   - TAM + monetization clarity check

3. Score against strict criteria (all 0-10):
   - **Novelty:** Would an expert say "I've never thought of that"?
   - **Validation:** Can we find real companies with this pain?
   - **Build complexity:** Can we MVP in 2 weeks?
   - **Moat potential:** Why won't competitors crush us?

4. **If average score ≥ 8:** Notify Austin, await approval
5. **If average score < 8:** Log to SCRATCHPAD.md, loop (max 5 iterations per run)

**Files:**
- `SCRATCHPAD.md` — Accumulated learnings, failed attempts
- `OPPORTUNITIES.md` — Validated opportunities
- `STATE.json` — Current state, pending approvals

### 2. PRODUCT (Triggered by approval)

**Goal:** Define complete product spec + GTM strategy

**Process:**
1. Read approved opportunity from STATE.json
2. Research competitors, pricing, positioning
3. Define MVP scope (2-week build target)
4. Define monetization strategy
5. Define target audience + messaging
6. Write PRODUCT_SPEC.md
7. Notify Austin for approval

**Output:**
- `projects/[project]/PRODUCT_SPEC.md`
- Updates to JOB_BOARD.json (adds to both queues when approved)

### 3. BUILD (Every 15 minutes)

**Goal:** Execute on product specs, ship MVPs

**Process:**
1. Check JOB_BOARD.json for `build_queue` items
2. Pick highest priority "in_progress" or "queued" project
3. Read project's PRODUCT_SPEC.md and BUILD_LOG.md
4. Execute next task:
   - Scaffold project structure
   - Build features
   - Write tests
   - Run tests
   - Fix failures
   - Security review
   - Integration testing

5. Ralph Wiggum loop until task passes or escalation exhausted
6. Update BUILD_LOG.md with progress
7. When MVP complete: notify Austin, await approval

**Files:**
- `projects/[project]/BUILD_LOG.md` — Progress and failures
- `JOB_BOARD.json` — Queue management

### 4. GTM (Every 15 minutes, parallel to Build)

**Goal:** Prepare marketing and sales assets

**Process:**
1. Check JOB_BOARD.json for `gtm_queue` items
2. Pick highest priority project
3. Read PRODUCT_SPEC.md for positioning
4. Work through checklist:
   - Google Ads (keywords, ad copy, budget)
   - Meta Ads (audiences, creatives, copy)
   - Cold Email (Instantly sequence)
   - Cold Calling (script, lead list)

5. Save assets to `projects/[project]/gtm/`
6. When complete: notify Austin, await approval

**Files:**
- `projects/[project]/gtm/` — All GTM assets
- `projects/[project]/GTM_PLAN.md` — Status and checklist

### 5. LAUNCH (Human-triggered)

**Prerequisites:**
- Build approved
- GTM approved

**Actions:**
- Deploy to production
- Activate ad campaigns
- Start cold outreach
- Monitor initial metrics

## State Management

### STATE.json Schema
```json
{
  "phase": "building",           // research | product | building | launching
  "pending_approval": null,      // {type: "research|product|build|gtm", ...}
  "research": {
    "iterations": 0,
    "last_run": "ISO timestamp"
  },
  "active_projects": ["aiservicecalls", "paidup"],
  "notifications_pending": [],
  "paused": false
}
```

### JOB_BOARD.json Schema
```json
{
  "build_queue": [
    {
      "project": "aiservicecalls",
      "status": "in_progress",    // queued | in_progress | review | approved | blocked
      "priority": 1,
      "spec_path": "projects/deep-water/PRODUCT_SPEC.md",
      "started_at": "ISO timestamp",
      "last_activity": "ISO timestamp"
    }
  ],
  "gtm_queue": [
    {
      "project": "paidup",
      "status": "in_progress",
      "priority": 1,
      "started_at": "ISO timestamp",
      "last_activity": "ISO timestamp"
    }
  ]
}
```

## Approval Commands

Austin can send these commands via Telegram:

| Command | Action |
|---------|--------|
| `approve [opportunity]` | Create PRODUCT_SPEC task |
| `approve spec [project]` | Add to build_queue and gtm_queue |
| `approve mvp [project]` | Mark build complete |
| `approve gtm [project]` | Mark GTM complete |
| `launch [project]` | Go live (both must be approved) |
| `reject [x]` | Log feedback, reset state |
| `pause` | Pause all crons |
| `resume` | Resume all crons |
| `status` | Report current state |

## Model Strategy

| Task | Default Model | Escalation |
|------|--------------|------------|
| Data collection | Sonnet | Opus after 2 fails |
| Synthesis | Opus | Opus + thinking |
| Boilerplate code | Sonnet | Opus after 3 fails |
| Complex logic | Opus | Opus + thinking |
| GTM copy | Sonnet | Opus for refinement |

## Ralph Wiggum Protocol

See `RALPH_WIGGUM.md` for the persistence protocol that powers all agents.

## Current Projects

| Project | Stage | Priority |
|---------|-------|----------|
| aiservicecalls (Deep Water) | Build | 1 |
| paidup | GTM prep | 1 |
| insurance (Texas OSSF) | Research validation | 2 |

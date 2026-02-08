# Opportunity Engine Approval Commands

When Austin sends these commands (via Telegram, Discord, or direct chat), process them accordingly.

## Command Reference

### Research Approvals

**`approve [opportunity-name]`**
1. Read `projects/opportunity-engine/OPPORTUNITIES.md` to find the opportunity
2. Update `STATE.json`:
   ```json
   {
     "phase": "product",
     "pending_approval": null
   }
   ```
3. Spawn Product Agent (use prompts/PRODUCT_AGENT.md)
4. Reply: "✅ Approved. Starting product spec for [opportunity-name]..."

### Product Spec Approvals

**`approve spec [project]`**
1. Update `JOB_BOARD.json`:
   - Add to `build_queue` with priority 1, status "in_progress"
   - Add to `gtm_queue` with priority based on existing items
2. Update `STATE.json`:
   ```json
   {
     "phase": "building",
     "active_projects": ["[project]", ...existing],
     "pending_approval": null
   }
   ```
3. Reply: "✅ Spec approved. [project] added to Build and GTM queues."

### Build Approvals

**`approve mvp [project]`**
1. Update `JOB_BOARD.json`: set build_queue item status to "approved"
2. Check if GTM is also approved for this project
3. If both approved:
   - Update `STATE.json`: phase = "ready_to_launch"
   - Reply: "✅ MVP approved. GTM also ready. Reply 'launch [project]' to go live."
4. If GTM pending:
   - Reply: "✅ MVP approved. Waiting on GTM completion."

### GTM Approvals

**`approve gtm [project]`**
1. Update `JOB_BOARD.json`: set gtm_queue item status to "approved"
2. Check if Build is also approved for this project
3. If both approved:
   - Update `STATE.json`: phase = "ready_to_launch"
   - Reply: "✅ GTM approved. Build also ready. Reply 'launch [project]' to go live."
4. If Build pending:
   - Reply: "✅ GTM approved. Waiting on MVP completion."

### Launch

**`launch [project]`**
1. Verify both build and GTM are approved in JOB_BOARD.json
2. Execute launch checklist:
   - Deploy to production (if not already live)
   - Activate ad campaigns
   - Start cold email sequences
   - Update project status to "launched"
3. Remove from queues
4. Reply with launch summary and monitoring links

### Rejections

**`reject [x]`** or **`reject [x] [feedback]`**
1. Log rejection with feedback to `SCRATCHPAD.md`
2. Reset `STATE.json` pending_approval to null
3. If rejecting research: Research agent will try again next run
4. If rejecting spec: Product agent needs to revise
5. If rejecting build/gtm: Send feedback back to relevant agent
6. Reply: "📝 Rejected. Feedback logged. Agent will revise."

### Control Commands

**`pause`**
1. Update `STATE.json`: `"paused": true`
2. All cron agents check this flag and skip execution
3. Reply: "⏸️ Opportunity Engine paused. Use 'resume' to continue."

**`resume`**
1. Update `STATE.json`: `"paused": false`
2. Reply: "▶️ Opportunity Engine resumed."

**`status`**
Generate and reply with:
```
📊 Opportunity Engine Status

Phase: [phase]
Paused: [yes/no]

Build Queue:
- [project]: [status] (priority [N])
- ...

GTM Queue:
- [project]: [status] (priority [N])
- ...

Pending Approval: [type] - [details]

Last Research Run: [timestamp]
Research Iterations: [N]
```

## State Transitions

```
                    ┌──────────┐
                    │ RESEARCH │
                    └────┬─────┘
                         │ approve [opportunity]
                         ▼
                    ┌──────────┐
                    │ PRODUCT  │
                    └────┬─────┘
                         │ approve spec [project]
                         ▼
              ┌──────────┴──────────┐
              │      BUILDING       │
              │  (parallel queues)  │
              └──────────┬──────────┘
                         │ approve mvp + approve gtm
                         ▼
                 ┌───────────────┐
                 │ READY_TO_LAUNCH│
                 └───────┬───────┘
                         │ launch [project]
                         ▼
                    ┌──────────┐
                    │ LAUNCHED │
                    └──────────┘
```

## Integration Notes

The main agent should:
1. Watch for these command patterns in messages from Austin
2. Execute the corresponding state updates
3. Reply with confirmation
4. The cron agents will pick up the new state on their next run

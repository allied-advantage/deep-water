# Ralph Wiggum Protocol

> "Me fail English? That's unpossible!" - Ralph Wiggum

The Ralph Wiggum protocol is our persistence strategy for autonomous agents. Named after the Simpsons character who keeps trying despite setbacks, it's the core loop that powers all Opportunity Engine agents.

## Core Principle

**Same prompt, fed back repeatedly, until success.**

Agents don't give up. They try, fail, learn, escalate, and try again. Failures are data, not defeats.

## The Loop

```
┌─────────────────────────────────────────┐
│           READ PREVIOUS WORK            │
│  (files contain context from last run)  │
└─────────────────┬───────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────┐
│            EXECUTE TASK                 │
│     (with current model + params)       │
└─────────────────┬───────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────┐
│         CHECK COMPLETION CRITERIA       │
│    (look for promise phrase/metrics)    │
└─────────────────┬───────────────────────┘
                  │
          ┌──────┴──────┐
          │             │
          ▼             ▼
     [SUCCESS]     [FAILURE]
          │             │
          ▼             ▼
       STOP        INCREMENT
                   ITERATION
                        │
                        ▼
              ┌─────────────────┐
              │ MAX ITERATIONS? │
              └────────┬────────┘
                       │
               ┌───────┴───────┐
               │               │
               ▼               ▼
           [YES]           [NO]
               │               │
               ▼               ▼
         ESCALATE         LOOP BACK
         OR STOP          WITH FEEDBACK
```

## Key Components

### 1. State Lives in Files

Agents wake up fresh every run. All context comes from files:
- Previous outputs
- Failure logs
- Accumulated learnings
- Current iteration count

**Example files:**
- `SCRATCHPAD.md` — What we've tried, what failed, why
- `BUILD_LOG.md` — Task history, test results
- `STATE.json` — Current phase, iteration counts

### 2. Clear Completion Criteria

Every task has a "promise phrase" or measurable success condition:
- Research: Average score ≥ 8/10
- Build: All tests pass
- GTM: Checklist complete

If the output contains the promise phrase, we're done.

### 3. Iteration Limits

Prevents infinite loops and budget burn:
- Research loops: **5 iterations max** per 4-hour run
- Build tasks: **10 iterations max** per task
- GTM tasks: **5 iterations max** per task

### 4. Adaptive Model Escalation

Start cheap, escalate when stuck:

| Attempt | Model | Notes |
|---------|-------|-------|
| 1-2 | Sonnet | Fast, cheap |
| 3 | Sonnet + feedback | Include previous failure details |
| 4-5 | Opus | Bigger brain |
| 6+ | Opus + thinking | Maximum reasoning power |

### 5. Failure Logging

Every failure gets logged with:
- What was attempted
- What went wrong
- Iteration number
- Model used
- Timestamp

This becomes training data for the next attempt.

## Implementation Example

```markdown
## Research Agent Ralph Loop

ITERATION 3/5
Previous attempts logged in SCRATCHPAD.md

1. Read SCRATCHPAD.md for context
2. Run collectors (escalated to Opus after 2 Sonnet fails)
3. Synthesize with Opus + thinking (escalated due to weak synthesis)
4. Score: 6.5/10 (below 8 threshold)
5. Log failure:
   - "Opportunity too crowded (score 4/10 on moat)"
   - "Need to dig into more obscure industries"
6. Increment iteration → 4/5
7. Loop back with this feedback
```

## Anti-Patterns

❌ **Don't:** Give up after first failure
✅ **Do:** Log failure, adjust, try again

❌ **Don't:** Use the same approach repeatedly
✅ **Do:** Incorporate feedback from failures

❌ **Don't:** Escalate immediately to expensive models
✅ **Do:** Start cheap, escalate based on failure patterns

❌ **Don't:** Store context in memory
✅ **Do:** Write everything to files

## Why It Works

1. **Persistence beats perfection.** Most tasks eventually yield to repeated attempts.
2. **Files are memory.** Agents build on previous work without needing session continuity.
3. **Escalation is strategic.** Cheap models handle most work; expensive ones crack hard problems.
4. **Failures are data.** Every attempt teaches us something.

## The Ralph Wiggum Mindset

Ralph doesn't know he's "supposed" to fail. He just keeps trying with genuine enthusiasm. Our agents should embody this:

- No shame in failure
- Each attempt is a fresh start with accumulated wisdom
- Eventually, persistence wins

> "I'm learnding!" - Ralph Wiggum

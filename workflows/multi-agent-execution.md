# CodeFoundry Version 1.0.1 — Multi-Agent Execution Workflow

## Purpose

This workflow defines how CodeFoundry coordinates independent specialist agents while keeping lifecycle authority centralized in the orchestrator.

## 1. Execution cycle

```text
READ STATE
  ↓
BUILD TASK GRAPH
  ↓
CLASSIFY DEPENDENCIES
  ↓
ACTIVATE SPECIALISTS
  ↓
RUN INDEPENDENT TASKS IN PARALLEL
  ↓
COLLECT RESULTS
  ↓
VALIDATE / RECONCILE
  ↓
UPDATE STATE + EVENT LOG
  ↓
CHECK GATES / RE-ENTRY
  ↓
CREATE NEXT TASK GRAPH
```

## 2. Task graph

A task is executable only when:

- its prerequisites are complete,
- required inputs exist,
- its owner is available,
- no higher-priority blocker prevents it.

Example:

```text
Product: define user/problem ──────┐
                                   ├─→ Engineering: technical plan
Research: competitor evidence ─────┘
                                   └─→ Security: threat review

Engineering plan ─→ Human technical-plan gate ─→ Implementation
Implementation ─→ QA verification ─────────────→ Review
```

Independent Product and Research tasks can run concurrently. Engineering consumes their accepted outputs. Implementation waits for required approvals.

## 3. Dependency types

- `REQUIRES_ARTIFACT` — task needs a specific artifact revision.
- `REQUIRES_DECISION` — task needs an explicit decision.
- `REQUIRES_GATE` — task cannot start until a gate passes.
- `REQUIRES_AGENT_RESULT` — task consumes another agent's result.
- `BLOCKED_BY_RISK` — execution is paused by an unresolved risk.
- `CONFLICT` — another task has an incompatible write or decision.

## 4. Agent contract

Each specialist receives:

- task ID
- lifecycle phase
- objective
- accepted inputs
- constraints
- expected output
- evidence requirements
- dependency context

Each specialist returns:

- task ID
- owner
- status
- result summary
- artifacts produced/updated
- evidence
- assumptions introduced
- risks discovered
- blockers
- recommended next action

A specialist cannot declare a lifecycle phase complete or approve its own consequential gate.

## 5. Concurrency controls

### Safe to parallelize

Examples:

- market research + technical feasibility research
- independent competitor research streams
- QA test design + documentation review
- security threat modeling + non-conflicting product analysis

### Must serialize

Examples:

- implementation after technical-plan approval
- security verification after the relevant security-sensitive implementation exists
- release after required testing and review
- two agents editing the same authoritative artifact
- any work whose outcome depends on an unresolved human decision

## 6. Conflict handling

When two agents produce conflicting recommendations:

1. Preserve both results.
2. Mark the conflict explicitly.
3. Identify the decision owner.
4. Ask for additional evidence if needed.
5. Escalate to a human gate when the decision is consequential.
6. Do not silently choose one result merely because it arrived first.

## 7. Failure handling

A failed task must remain visible.

```text
RUNNING
  ↓
FAILED
  ├─ retry permitted → RUNNING
  ├─ dependency affected → BLOCKED
  ├─ design invalidated → RE-ENTRY
  └─ consequential decision required → HUMAN GATE
```

Retries must not erase the original failure evidence.

## 8. Deadlock and livelock protection

The orchestrator must detect:

- circular dependencies,
- repeated retries without new evidence,
- agents repeatedly handing the same task to each other,
- tasks waiting indefinitely for unavailable dependencies,
- conflicting writers repeatedly invalidating each other.

When detected, stop the loop, preserve evidence, and surface a blocker for resolution.

## 9. Authority boundaries

```text
SPECIALIST AGENT
    │
    ├─ produces evidence
    ├─ produces recommendations
    ├─ produces artifacts
    └─ reports blockers
             │
             ▼
       ORCHESTRATOR
             │
    ┌────────┴────────┐
    ▼                 ▼
STATE CHANGE      HUMAN GATE
```

Only the orchestrator changes lifecycle state. Human decisions are recorded as decisions, not inferred from agent consensus.

## 10. Host/runtime boundary

CodeFoundry defines this protocol but does not assume a particular process model.

A host may implement each specialist as:

- a separate agent session,
- a worker process,
- a queued job,
- a remote agent,
- a container,
- or another isolated execution identity.

The contract remains the same: independent ownership, explicit dependencies, durable results, and centralized lifecycle authority.

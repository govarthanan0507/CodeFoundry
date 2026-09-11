# CodeFoundry Version 1.0.1 — Task Ledger Contract

The task ledger is the durable execution record for specialist work.

## Task schema

```yaml
task_id: "TASK-0001"
phase: "REQUIREMENTS"
owner: "product"
objective: ""
status: "READY"
priority: "NORMAL"
dependencies: []
inputs: []
expected_outputs: []
started_at: ""
completed_at: ""
evidence: []
artifacts: []
assumptions: []
risks: []
blockers: []
failure:
  count: 0
  last_error: ""
  retry_allowed: false
```

## Status semantics

| Status | Meaning |
|---|---|
| READY | Eligible to run when scheduled |
| RUNNING | Agent is actively working |
| BLOCKED | Cannot proceed because of a blocker |
| WAITING_FOR_AGENT | Waiting for another agent result |
| WAITING_FOR_HUMAN | Waiting for a human decision/gate |
| SUCCEEDED | Work completed and result returned |
| FAILED | Work failed; evidence retained |
| CANCELLED | Explicitly stopped |
| SUPERSEDED | Replaced by newer work |

## Rules

1. Every material task has exactly one owner at a time.
2. A task cannot become RUNNING while a required dependency is unresolved.
3. A task cannot become SUCCEEDED without a result and evidence location.
4. Failed tasks remain in history.
5. Retries create additional execution evidence rather than erasing failure history.
6. A task may be superseded only with a recorded reason and replacement task.
7. Only the orchestrator may change lifecycle phase.
8. Human-gated tasks remain WAITING_FOR_HUMAN until explicit approval is recorded.

# CodeFoundry Version 1.0.1 — Event Log Contract

The event log records material lifecycle and execution events. It is an audit trail, not a replacement for project state.

## Event schema

```yaml
event_id: "EVT-0001"
timestamp: ""
type: "TASK_COMPLETED"
phase: "REQUIREMENTS"
actor: "product"
task_id: "TASK-0001"
summary: "Requirements draft completed"
artifacts: []
evidence: []
risk_change: ""
state_change: ""
correlation_id: ""
```

## Required event types

- `PROJECT_INITIALIZED`
- `SPECIALIST_ACTIVATED`
- `TASK_STARTED`
- `TASK_COMPLETED`
- `TASK_FAILED`
- `DEPENDENCY_BLOCKED`
- `ARTIFACT_PRODUCED`
- `ARTIFACT_INVALIDATED`
- `RISK_DISCOVERED`
- `GATE_SUBMITTED`
- `HUMAN_APPROVAL_REQUESTED`
- `HUMAN_DECISION_RECORDED`
- `PHASE_CHANGED`
- `REENTRY_TRIGGERED`
- `RELEASE_MILESTONE`
- `DEPLOYMENT_MILESTONE`

## Event rules

1. Events are append-oriented; history must not be silently rewritten.
2. Events describe what happened, not what should have happened.
3. Every event must identify an actor.
4. Consequential state changes must have an associated event.
5. Low-level command output belongs in drill-down evidence, not the milestone stream.
6. Event summaries must be understandable to a human without reading raw logs.

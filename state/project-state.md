# CodeFoundry Version 1.0.1 — Project State

Use this template as the durable state contract for a project managed by CodeFoundry.

```yaml
project:
  name: ""
  description: ""
  created_at: ""
  lifecycle_version: "1.0.1"

lifecycle:
  current_phase: "IDEA"
  current_state: "DRAFT"
  previous_phase: ""
  next_action: ""

risk:
  level: "UNKNOWN"
  rationale: ""

roles:
  active: []

execution:
  progress_summary: ""
  status_updated_at: ""
  active_tasks: []
  blocked_tasks: []
  waiting_tasks: []
  recent_events: []

tasks:
  ledger: []

events:
  log: []

artifacts:
  completed: []
  pending: []

assumptions:
  active: []
  resolved: []

risks:
  open: []
  accepted: []

questions:
  open: []
  resolved: []

decisions:
  pending: []
  approved: []
  rejected: []
  superseded: []

gates:
  pending: []
  passed: []
  failed: []

traceability:
  intent: ""
  requirements: []
  decisions: []
  implementation: []
  tests: []
  release: []
  production: []
```

## State rules

- State must reflect reality, not the desired outcome.
- A phase is not marked complete until its required work and gate conditions are satisfied.
- Rejected decisions remain visible.
- Superseded decisions remain visible for history.
- Open risks remain visible until resolved or explicitly accepted.
- Every material state change must be attributable to a meaningful event or decision.
- Every material task must have an owner and execution state.
- A blocked or waiting task must identify what it is waiting for.
- Current progress must be understandable without reconstructing the conversation.
- Progress percentages are approximate unless a deterministic measurement exists.
- The task ledger and event log provide execution history; lifecycle state remains the authoritative current snapshot.

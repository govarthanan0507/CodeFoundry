# CodeFoundry V1 — Project State

Use this template as the durable state contract for a project managed by CodeFoundry.

```yaml
project:
  name: ""
  description: ""
  created_at: ""
  lifecycle_version: "V1"

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
- Every state change should be attributable to a meaningful event or decision.
- The current next action must be understandable without reconstructing the entire conversation.
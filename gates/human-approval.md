# Human Approval Gate — V1

## Purpose

Human approval is the control boundary for consequential judgment.

## Gate states

```text
DRAFT
  ↓
SUBMITTED
  ↓
AGENT_REVIEW
  ↓
HUMAN_REVIEW
  ├── APPROVED → EXECUTING
  ├── REJECTED → REVISION
  └── BLOCKED → RESOLVE BLOCKER
```

## Minimum gate record

```text
GATE:
PHASE:
ARTIFACT:
DECISION:
DECISION MAKER:
DATE:
EVIDENCE:
RISKS:
CONDITIONS:
NEXT ACTION:
```

## Approval rules

1. Approval must be explicit.
2. Approval must refer to the artifact or decision being approved.
3. Approval does not erase unresolved risks unless those risks are explicitly accepted.
4. A rejected artifact returns to revision.
5. A changed artifact may require a new approval.
6. A later material change invalidates earlier approval where the changed decision is affected.
7. The system must never infer approval from silence.

## Typical mandatory gates

- product direction
- validation outcome
- material naming/identity decision
- requirements
- architecture
- material security/privacy risk
- technical plan for consequential work
- release readiness
- consequential production deployment

Risk and project type determine whether additional gates are necessary.

## Gate failure

A failed gate is useful evidence. It should result in a recorded reason and a clear next action, not a hidden retry loop.

## Escalation

Some decisions may require a different authority, such as legal, security, compliance, finance, or operations. CodeFoundry should identify the required authority rather than pretending the normal human gate is sufficient.
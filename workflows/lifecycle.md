# CodeFoundry Version 1.0.1 — Lifecycle Workflow

## 1. Purpose

This document defines the lifecycle CodeFoundry uses to decide what should happen next and how work is executed by specialist agents.

The lifecycle is a directed graph with controlled re-entry, not a one-way checklist.

```text
IDEA
 ↓
PROBLEM
 ↓
TARGET USER
 ↓
VALIDATION
 ↓
CONCEPT
 ↓
NAMING
 ↓
NAME VALIDATION
 ↓
MARKET / COMPETITOR RESEARCH
 ↓
FEASIBILITY
 ↓
REQUIREMENTS
 ↓
PRODUCT DEFINITION
 ↓
ARCHITECTURE
 ↓
SECURITY / PRIVACY
 ↓
TECHNICAL PLAN
 ↓
IMPLEMENTATION
 ↓
TESTING
 ↓
REVIEW
 ↓
INTEGRATION
 ↓
STAGING
 ↓
RELEASE READINESS
 ↓
DEPLOYMENT
 ↓
PRODUCTION
 ↓
MONITORING
 ↓
INCIDENT / IMPROVEMENT
 ↺ NEXT ITERATION
```

## 2. Universal stage procedure

For every meaningful stage:

1. Read current project state.
2. Read accepted upstream artifacts.
3. Identify the stage objective.
4. Identify known facts.
5. Identify assumptions and unknowns.
6. Identify risks and dependencies.
7. Determine whether research is required.
8. Build the task graph.
9. Activate relevant specialist agents.
10. Run independent tasks in parallel where safe.
11. Collect and validate specialist results.
12. Produce or update the required artifact.
13. Validate the artifact.
14. Determine whether a human gate applies.
15. Stop if approval is required and not yet granted.
16. Record the decision.
17. Update project state and meaningful event history.
18. Determine the next stage and task set.

## 3. Stage registry

| Stage | Objective | Typical output | Gate intensity |
|---|---|---|---|
| Idea | Capture raw intent | intent | Human framing |
| Problem | Establish the actual problem | problem section | Human confirmation |
| Target User | Identify intended users | user definition | Human confirmation |
| Validation | Test assumptions and demand | validation | Human decision |
| Concept | Define product concept | concept | Human approval |
| Naming | Generate candidate identity | candidates | Human choice |
| Name Validation | Research conflicts | evidence | Human/legal escalation where needed |
| Market / Competitor Research | Understand alternatives | research evidence | Human positioning decision |
| Feasibility | Determine whether pursuit is sensible | feasibility assessment | Human investment decision |
| Requirements | Define behavior and constraints | requirements.md | Approval |
| Product Definition | Define scope and success | product boundary | Approval |
| Architecture | Define technical structure | architecture evidence | Approval |
| Security / Privacy | Identify and control security/privacy risk | security evidence | Approval for material risks |
| Technical Plan | Turn design into work | plan.md | Approval |
| Implementation | Build | code + implementation evidence | Risk-based |
| Testing | Verify behavior | test evidence | Quality gate |
| Review | Independent challenge | review findings | Gate |
| Integration | Consolidate accepted work | integrated state | Gate |
| Staging | Validate deployment path | staging evidence | Gate |
| Release Readiness | Prove release can proceed | release evidence | Human release gate |
| Deployment | Promote safely | deployment evidence | Human for consequential production changes |
| Production | Operate | production evidence | Operational |
| Monitoring | Observe system and outcomes | monitoring evidence | Operational |
| Incident / Improvement | Convert production evidence into action | incident/improvement record | Risk-based |

## 4. Parallel execution

Version 1.0.1 separates lifecycle authority from specialist execution.

Independent work may run concurrently when:

- dependencies are satisfied,
- outputs are independently producible,
- writes do not conflict,
- concurrency does not introduce a safety or correctness risk.

Work must be serialized when it consumes another task's output, requires a human gate, or would create an authoritative write conflict.

See `workflows/multi-agent-execution.md` for the execution contract.

## 5. Risk-based depth

Not every project needs the same ceremony.

Low-risk work may use lightweight artifacts and a small number of gates.

High-risk work may require additional:

- security review
- privacy review
- architecture review
- performance testing
- legal review
- compliance review
- operational readiness
- rollback validation
- independent review

Risk changes the amount of work, not the rule that consequential decisions require appropriate authority.

## 6. Re-entry rules

A later discovery can invalidate an earlier stage.

Examples:

```text
Testing → architecture issue → Architecture
```

```text
Market research → positioning problem → Validation / Concept
```

```text
Security review → unacceptable risk → Architecture / Requirements
```

```text
Production incident → requirement change → Next Iteration
```

When returning to an earlier stage:

1. Preserve the previous artifact.
2. Record why re-entry occurred.
3. Mark affected decisions as superseded or under review.
4. Create a new revision.
5. Identify downstream tasks invalidated by the change.
6. Re-run downstream gates affected by the change.

## 7. Completion rule

A stage is not complete merely because an agent generated text or code.

It is complete when:

- required work was performed,
- important unknowns were addressed or explicitly accepted,
- required evidence exists,
- the artifact is complete enough for the stage,
- blockers are resolved or explicitly escalated,
- required human approval exists,
- downstream tasks are not relying on invalidated inputs.

## 8. Progress rule

Human-facing progress is milestone-based.

Report:

- current phase,
- active specialist work,
- completed milestones,
- blockers and waits,
- material risks,
- next gate,
- next action.

Do not make raw commands, file edits, or tool telemetry the primary progress stream.

## 9. Production feedback loop

Production is not the end.

```text
PRODUCTION
   ↓
OBSERVATION
   ↓
INCIDENT / FEEDBACK / OPPORTUNITY
   ↓
NEW OR REVISED INTENT
   ↓
VALIDATION
   ↓
REQUIREMENTS
   ↓
PLAN
   ↓
IMPLEMENT
   ↓
TEST
   ↓
RELEASE
   ↓
PRODUCTION
```

This is the long-term closed loop CodeFoundry is intended to control.
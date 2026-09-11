# CodeFoundry V1 — Lifecycle Workflow

## 1. Purpose

This document defines the V1 lifecycle that CodeFoundry uses to decide what should happen next.

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
8. Activate relevant specialists.
9. Perform the stage work.
10. Produce or update the required artifact.
11. Validate the artifact.
12. Determine whether a human gate applies.
13. Stop if approval is required and not yet granted.
14. Record the decision.
15. Update project state.
16. Determine the next stage.

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

## 4. Risk-based depth

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

## 5. Re-entry rules

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
5. Re-run downstream gates affected by the change.

## 6. Completion rule

A stage is not complete merely because an agent generated text.

It is complete when:

- required work was performed,
- important unknowns were addressed or explicitly accepted,
- required evidence exists,
- the artifact is complete enough for the stage,
- blockers are resolved or explicitly escalated,
- required human approval exists.

## 7. Production feedback loop

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
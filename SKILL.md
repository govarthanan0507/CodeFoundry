---
name: codefoundry
description: >
  Orchestrates software work through a controlled production lifecycle from
  idea to production and continuous improvement using durable artifacts,
  evidence discipline, specialist routing, independent agent execution,
  human approval gates, risk management, progress observability, and
  traceability. Use when starting, planning, building, testing, reviewing,
  releasing, deploying, operating, or improving a software project.
---

# CodeFoundry — Production SDLC Orchestrator

## Purpose

CodeFoundry is a reusable SDLC control-plane skill. It determines what work should happen next, coordinates the appropriate specialist agents, preserves durable project state, exposes meaningful progress, and stops at consequential human approval boundaries.

> **The system decides what needs to happen next. The human decides whether that step is approved.**

## Version

**Version 1.0.1** — Multi-Agent Execution & Progress Observability.

Version 1.0.1 extends the V1 foundation with an explicit multi-agent execution protocol, task/dependency coordination, event-based progress reporting, blocked/waiting states, and human-readable status. It remains a host-agnostic skill contract; the host/runtime is responsible for actually creating and scheduling agent processes or sessions.

## Operating contract

When this skill is active:

1. Read current project state before acting.
2. Read accepted upstream artifacts before downstream decisions.
3. Determine the current lifecycle phase and next valid action.
4. Distinguish verified facts, user-provided facts, observations, assumptions, inferences, recommendations, decisions, and risks.
5. Research externally verifiable claims when they materially affect a decision; never fabricate evidence.
6. Activate only the specialist agents required by the current work and risk.
7. Prefer independent specialist work in parallel when dependencies allow it.
8. Give every material task an owner, status, dependency set, and expected output.
9. Produce durable artifacts for meaningful lifecycle work.
10. Validate artifacts before treating them as accepted inputs.
11. Never silently skip a mandatory gate.
12. Never infer human approval from silence, inactivity, vague praise, or unrelated approval.
13. Preserve rejected and superseded decisions and keep unresolved risks visible.
14. Re-enter earlier lifecycle stages when new evidence materially invalidates an accepted assumption, requirement, design, or decision.
15. Publish meaningful milestone/status events instead of exposing raw execution telemetry as the primary user experience.
16. Surface blocked work, failed work, dependency waits, and human waits explicitly.
17. Record consequential decisions and update state after material work.
18. Stop when a human approval gate requires judgment.
19. Keep the current status and next action understandable without reconstructing the conversation.

## Automatic initiation

When the user introduces a new software idea or objective:

1. Determine whether this is a new or existing project.
2. Initialize project state if needed.
3. Start at IDEATION unless accepted artifacts establish a later phase.
4. Identify facts, assumptions, unknowns, risks, dependencies, and decisions.
5. Route only the specialist agents required for the current stage.
6. Run independent work in parallel when safe and useful.
7. Create the appropriate durable artifact.
8. Validate the artifact.
9. Evaluate the applicable human gate.
10. Stop for human approval when required.
11. Record the decision and update state.
12. Create the next task set and determine the next valid action.

## Lifecycle

```text
IDEA
→ PROBLEM
→ TARGET USER
→ VALIDATION
→ CONCEPT
→ NAMING
→ NAME VALIDATION
→ MARKET / COMPETITOR RESEARCH
→ FEASIBILITY
→ REQUIREMENTS
→ PRODUCT DEFINITION
→ ARCHITECTURE
→ SECURITY / PRIVACY
→ TECHNICAL PLAN
→ IMPLEMENTATION
→ TESTING
→ REVIEW
→ INTEGRATION
→ STAGING
→ RELEASE READINESS
→ DEPLOYMENT
→ PRODUCTION
→ MONITORING
→ INCIDENT / IMPROVEMENT
→ NEXT ITERATION
```

The lifecycle is a directed graph, not an irreversible linear pipeline.

## Multi-agent execution model

Specialist roles are independent work identities, not merely headings inside the orchestrator's reasoning.

```text
                         HUMAN
                           │
                           ▼
                    ORCHESTRATOR
                           │
          ┌────────────────┼────────────────┐
          ▼                ▼                ▼
       PRODUCT          RESEARCH       ENGINEERING
          │                │                │
          └────────────────┼────────────────┘
                           ▼
                           QA
                           │
                           ▼
                        SECURITY
                           │
                           ▼
                     ORCHESTRATOR
                           │
                           ▼
                      HUMAN GATE
```

The orchestrator owns lifecycle authority. Specialists own scoped work. Specialists must return structured evidence and artifacts rather than silently changing lifecycle state.

### Parallelism rule

Run tasks concurrently when:

- they have no unresolved dependency on each other,
- their outputs can be independently produced,
- concurrent work does not create conflicting writes,
- the work is safe to run concurrently.

Serialize work when:

- one task consumes another task's output,
- two agents would modify the same authoritative artifact,
- a gate decision is required,
- a shared resource creates a correctness risk,
- a security/safety condition requires ordered review.

### Ownership rule

Every active task must identify:

- task ID
- owner agent
- lifecycle phase
- objective
- dependencies
- input artifacts
- expected output
- status
- evidence location
- failure/blocker information

Only the orchestrator may change lifecycle phase or declare a gate passed.

## Progress observability

The primary human-facing status must describe lifecycle progress, not command-by-command telemetry.

Preferred status:

```text
CODEFOUNDRY
Project: <name>
Phase: <phase>
Progress: <approximate status>

CURRENTLY WORKING
🟢 <agent> — <meaningful work>
🟢 <agent> — <meaningful work>
⏳ <agent> — waiting for <dependency>

LAST COMPLETED
✓ <milestone>
✓ <milestone>

RISKS
⚠ <risk>

NEXT GATE
🔴 <gate or None>

NEXT ACTION
<one clear action>
```

Raw commands, shell output, timers, file-by-file edits, and internal execution traces may exist as drill-down evidence, but they are not the default progress interface.

### Meaningful events

Publish events for material changes such as:

- project initialized
- specialist activated
- task started
- task completed
- task failed
- dependency blocked
- research completed
- artifact produced
- artifact invalidated
- risk discovered
- gate submitted
- human approval requested
- human decision recorded
- phase changed
- re-entry triggered
- release/deployment milestone reached

Do not emit a milestone for every low-level command unless it materially changes project state or is needed for debugging evidence.

## Durable state

Project state must include, at minimum:

- current phase and state
- previous phase
- next action
- risk level and rationale
- active specialist agents
- task ledger
- task dependencies
- current progress summary
- recent meaningful events
- completed/pending artifacts
- assumptions active/resolved
- open/accepted risks
- open/resolved questions
- pending/approved/rejected/superseded decisions
- pending/passed/failed gates
- intent → requirements → decisions → implementation → tests → release → production traceability

State must distinguish at least these execution states:

```text
READY
RUNNING
BLOCKED
WAITING_FOR_AGENT
WAITING_FOR_HUMAN
SUCCEEDED
FAILED
CANCELLED
SUPERSEDED
```

## Artifacts

V1 core artifacts:

- `intent.md`
- `ideation.md`
- `validation.md`
- `requirements.md`
- `plan.md`

Version 1.0.1 adds execution/progress contracts under `execution/` and extends project state to track agent tasks, dependencies, events, and human-readable status.

## Specialist routing

Available V1 specialist agents:

- Orchestrator — lifecycle control, routing, gates, next action
- Product — problem, users, value, scope, requirements
- Research — evidence, market, competitors, naming, validation
- Engineering — technical feasibility, planning, implementation
- QA — verification, testing, quality evidence
- Security — security, privacy, threats, risk

Only required agents should be activated. Multiple agents may work concurrently when the dependency graph permits it.

## Human gates

Human gates are hard boundaries. Typical mandatory gates include:

- product direction
- validation outcome
- material naming decision
- requirements
- architecture
- material security/privacy risk
- consequential technical plan
- release readiness
- consequential production deployment

Approval rules:

1. Approval must be explicit.
2. Approval must be tied to a specific artifact or decision.
3. Unresolved risks remain visible unless explicitly accepted.
4. Rejection returns work to revision.
5. Material changes may require new approval.
6. Earlier approval can be invalidated by material changes.
7. Silence is never approval.

**Important:** implementation intent is not technical-plan approval. A request such as “build it now” authorizes intent to proceed but does not itself approve an unreviewed technical plan when a technical-plan gate applies.

## Evidence discipline

Material claims are classified as:

- Verified fact
- User-provided fact
- Observation
- Assumption
- Inference
- Recommendation
- Decision
- Risk

Externally verifiable information should be researched when it materially affects a decision.

Research evidence must not be presented as legal clearance, certification, approval, or other authority that the evidence does not establish.

## Re-entry

New evidence may force controlled re-entry into an earlier stage.

When re-entry occurs:

1. Preserve the prior artifact.
2. Record the trigger.
3. Mark affected decisions as superseded or under review.
4. Create a new revision.
5. Identify downstream tasks invalidated by the change.
6. Re-run affected gates before continuing.

## Progressive disclosure

Read the following only as needed:

- `workflows/lifecycle.md` — lifecycle, transitions, and stage completion
- `workflows/multi-agent-execution.md` — task graph, parallelism, dependencies, coordination
- `execution/task-ledger.md` — task contract and execution states
- `execution/event-log.md` — meaningful event contract
- `execution/status.md` — human-facing progress contract
- `gates/human-approval.md` — human gate contract
- `agents/*.md` — specialist role contracts
- `artifacts/*.md` — artifact templates
- `state/project-state.md` — durable state contract

## Prohibitions

CodeFoundry must not:

- silently skip mandatory gates
- fabricate research or evidence
- turn assumptions into facts
- infer approval from silence
- allow specialists to self-approve consequential gates
- hide failed tests or security findings
- erase rejected or superseded decisions
- present raw execution telemetry as proof of lifecycle completion
- claim production readiness without required evidence
- claim legal clearance without authoritative legal evidence
- allow one specialist to silently rewrite another specialist's authoritative output
- create circular agent work without detection and escalation

## Completion boundary

Version 1.0.1 is a reusable multi-agent SDLC coordination contract. It does **not** by itself provide:

- a hosted workflow engine
- automatic process spawning across every host
- a database-backed runtime
- a dashboard
- authentication
- billing
- distributed infrastructure
- autonomous production deployment

A compatible host/runtime may implement these capabilities around the CodeFoundry contracts.

## Version 1.0.1 acceptance target

The version is considered operationally useful only if a fresh software idea can demonstrate:

1. separate specialist work identities or host-managed specialist sessions,
2. parallel execution where dependencies allow it,
3. explicit task ownership and dependencies,
4. durable execution state,
5. meaningful milestone/status updates,
6. explicit blocked/waiting states,
7. drill-down evidence separated from human-facing status,
8. correct human approval boundaries,
9. technical-plan approval before implementation when required,
10. re-entry when later evidence invalidates earlier work.

Failure of the governance rules is a release blocker even if the generated software itself works.

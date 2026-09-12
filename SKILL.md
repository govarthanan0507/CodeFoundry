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

**Version 1.0.1** — Multi-Agent Execution & Progress Observability, with Ideation Phase 1 intake integration.

Version 1.0.1 extends the V1 foundation with an explicit multi-agent execution protocol, task/dependency coordination, event-based progress reporting, blocked/waiting states, and human-readable status. The Ideation Phase 1 integration adds disciplined intent extraction, targeted clarification, context retention, and preservation of user-provided references within the existing ideation artifact. It remains a host-agnostic skill contract; the host/runtime is responsible for actually creating and scheduling agent processes or sessions.

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
4. For a new idea, execute the existing **Ideation Phase 1 — Idea Intake** procedure before moving into problem framing or downstream analysis.
5. Identify facts, assumptions, unknowns, risks, dependencies, and decisions.
6. Route only the specialist agents required for the current stage.
7. Run independent work in parallel when safe and useful.
8. Create the appropriate durable artifact.
9. Validate the artifact.
10. Evaluate the applicable human gate.
11. Stop for human approval when required.
12. Record the decision and update state.
13. Create the next task set and determine the next valid action.

## Ideation Phase 1 — Idea Intake integration

Phase 1 remains part of the existing lifecycle. It is not a separate subsystem, research engine, or alternate artifact model.

### Objective

Turn a raw human idea into a faithful, structured understanding of that idea while preserving the user's own context and references. Phase 1 should help a beginner explain what they have in mind without exposing unnecessary SDLC terminology.

Phase 1 produces the existing `artifacts/ideation.md` artifact and prepares it for the existing Phase 1 gate.

### Conversation discipline

Use a high-value-question approach:

- First understand the user's intent before asking for detail.
- Identify only the missing information that materially changes the current understanding.
- Ask the smallest useful number of questions.
- Use **three critical questions as the normal upper bound for an initial clarification round**, not as a rigid quota.
- If an answer reveals a new material ambiguity, a later focused question is allowed.
- Do not repeat questions that have already been answered or explicitly rejected.
- Do not overwhelm the user with an SDLC questionnaire.
- Prefer plain-language questions such as who they imagine using it, what problem it should help with, what they have seen, or what constraints matter.

The governing principle is:

> **Do not ask the user something unless the answer can materially improve CodeFoundry's understanding of the idea.**

### Context retention

Maintain a Phase 1 context block containing, at minimum:

- original idea
- confirmed information
- user corrections or rejected interpretations
- current understanding
- important constraints
- unresolved questions
- user-provided references
- clarification history

This context is durable working information. It prevents the system from repeatedly asking the same question or silently changing its interpretation.

### User-provided references

The user may optionally provide material they want CodeFoundry to look at. Supported reference types include:

- website URL
- GitHub repository
- document or PDF
- screenshot
- app or product
- notes or research
- other relevant material

References are first-class records in the existing ideation artifact. They must preserve what the user said about why the reference matters.

A user-provided reference is **evidence of the user's interest or context, not proof of a product claim, market demand, feasibility, legal status, technical suitability, or competitor relationship**.

GitHub is simply one normal reference source. Phase 1 does not create a separate GitHub subsystem.

### Phase 1 boundary

Phase 1 may:

- capture the raw idea verbatim,
- extract and summarize intent,
- distinguish explicit user statements from inference,
- identify explicitly stated users and needs,
- capture constraints and exclusions,
- identify assumptions and unknowns,
- ask targeted clarification questions,
- collect and label user-provided references,
- preserve supplied research or notes,
- record understanding confidence,
- validate the Idea Intake artifact,
- determine whether the idea is ready for the next stage.

Phase 1 must **not** prematurely:

- decide whether the product should be built,
- validate market demand,
- perform full competitor or market analysis,
- make feasibility conclusions,
- define architecture or technology,
- produce requirements or an MVP,
- turn references into requirements,
- treat supplied examples as verified evidence,
- bypass later human gates.

Detailed analysis belongs to the later lifecycle stages that already exist in CodeFoundry.

### Specialist routing for Phase 1

Default routing is intentionally small:

- **Orchestrator** — controls the phase, context, questions, artifact, and gate.
- **Product** — used when product/user/need interpretation requires specialist support.
- **Research** — used only when the user has supplied references that need basic preservation/identification or when explicit external research is genuinely required by the current phase.

Engineering, QA, and Security are not activated merely because a user has an idea. They are introduced when their lifecycle stage or risk warrants them.

### Phase 1 quality check

Before submitting the existing Phase 1 gate, verify that:

1. The original idea is preserved.
2. User statements and CodeFoundry inferences are distinguishable.
3. The current understanding is faithful to the user's intent.
4. Important ambiguity has been surfaced rather than hidden.
5. Clarification questions were targeted and non-redundant.
6. Confirmed constraints and exclusions are preserved.
7. User-provided references are preserved with type, source, user description, intended relevance, and analysis status.
8. GitHub references use the same reference model as other sources.
9. No downstream market, feasibility, technical, validation, or implementation conclusion has been smuggled into Phase 1.
10. The artifact is sufficient for the next stage without requiring reconstruction of the conversation.

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
- `workflows/ideation-phase-1.md` — existing lifecycle Phase 1 execution procedure
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
- let Phase 1 turn user-provided references into unverified requirements or conclusions
- overwhelm a beginner with unnecessary lifecycle terminology or low-value questions

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
10. re-entry when later evidence invalidates earlier work,
11. Phase 1 can capture a raw idea into the existing ideation artifact without prematurely performing downstream analysis,
12. Phase 1 can preserve optional user-provided references, including GitHub repositories, as traceable context.

Failure of the governance rules is a release blocker even if the generated software itself works.

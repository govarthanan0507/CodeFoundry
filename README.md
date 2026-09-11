# CodeFoundry

**A generic production SDLC orchestration and control-plane skill.**

CodeFoundry is designed to take a software idea or software objective and guide it through a disciplined lifecycle: discovery, validation, requirements, architecture, implementation, testing, release, deployment, production operations, and continuous improvement.

> **The system decides what needs to happen next. The human decides whether that step is approved.**

---

## Current version

# Version 1.0.1 — Multi-Agent Execution & Progress Observability

Version 1.0.1 is the first execution-focused evolution of the V1 foundation. It keeps lifecycle authority centralized in the orchestrator while allowing independent specialist agents to work concurrently where dependencies permit.

It directly addresses two findings from the first real lifecycle exercise:

1. specialist roles were conceptual within one session instead of explicit independent work identities;
2. user-facing progress was too close to low-level execution telemetry.

It also closes the identified governance defect where implementation could occur before technical-plan approval.

---

## Why CodeFoundry exists

Software work often begins with implementation before the problem, users, risks, requirements, architecture, release strategy, or operational model are sufficiently understood.

CodeFoundry treats the SDLC as a controlled lifecycle rather than a coding prompt.

Instead of:

```text
Idea → Code → Bugs → Fixes → Deployment
```

it aims for:

```text
Idea
  ↓
Problem
  ↓
Users / Context
  ↓
Validation
  ↓
Concept
  ↓
Naming / Identity Validation
  ↓
Market / Competitor Research
  ↓
Feasibility
  ↓
Requirements
  ↓
Product Definition
  ↓
Architecture
  ↓
Security / Privacy
  ↓
Technical Plan
  ↓
Implementation
  ↓
Testing
  ↓
Review
  ↓
Integration
  ↓
Staging
  ↓
Release Readiness
  ↓
Deployment
  ↓
Production
  ↓
Monitoring
  ↓
Incidents / Improvement
  ↓
Next Iteration
```

The lifecycle is intentionally non-linear. Evidence discovered later can send a project back to an earlier stage.

---

## V1 foundation

The original V1 foundation established:

- automatic lifecycle initiation for new ideas
- explicit lifecycle stages
- durable artifact handoffs
- persistent project-state expectations
- dynamic specialist routing
- research-before-assertion discipline
- human approval gates
- rejection and revision paths
- traceability expectations
- production and post-production lifecycle coverage

The goal was to prove the control loop before adding execution infrastructure.

---

## Version 1.0.1 additions

### Independent specialist execution

Specialists are now defined as independent work identities rather than merely roles performed sequentially inside the orchestrator's reasoning.

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

The host/runtime may implement an agent as a separate session, worker process, queued job, container, remote agent, or another isolated execution identity.

### Parallel execution

Independent work can run concurrently when:

- dependencies are satisfied;
- outputs are independently producible;
- writes do not conflict;
- concurrency does not introduce a safety or correctness risk.

Dependent work must wait. Human-gated work must stop until explicit approval exists.

### Task ledger

Every material task now has:

- task ID
- owner
- phase
- objective
- dependencies
- inputs
- expected output
- status
- evidence
- blockers/failure information

Execution states include:

`READY`, `RUNNING`, `BLOCKED`, `WAITING_FOR_AGENT`, `WAITING_FOR_HUMAN`, `SUCCEEDED`, `FAILED`, `CANCELLED`, `SUPERSEDED`.

### Event-based progress

Meaningful lifecycle events are recorded for milestones such as task completion, blockers, artifact production, gate submission, human decisions, phase changes, and re-entry.

Raw shell commands, timers, file-by-file edits, and internal telemetry may remain available as drill-down evidence, but they are not the primary human-facing progress stream.

### Human-readable status

The preferred status answers:

1. Where are we?
2. What is happening now?
3. What finished?
4. What is blocked or waiting?
5. What risks matter?
6. What decision or action is next?

Example:

```text
CODEFOUNDRY
Project: Sleep Tracker
Phase: IMPLEMENTATION
Progress: 72%

CURRENTLY WORKING
🟢 Engineering — implementing authentication
🟢 QA — preparing regression tests
⏳ Security — waiting for authentication implementation

LAST COMPLETED
✓ Requirements approved
✓ Technical plan approved

RISKS
⚠ Hosting environment not selected

NEXT GATE
🔴 Security review

NEXT ACTION
Complete authentication and hand off to Security.
```

Progress percentages are approximate unless the lifecycle has a deterministic measurement model.

### Governance correction

Version 1.0.1 explicitly separates implementation intent from technical-plan approval.

```text
“Build it now”
        ≠
“Technical plan approved”
```

When a technical-plan gate applies, implementation must wait for explicit approval.

---

## Repository structure

```text
CodeFoundry/
│
├── SKILL.md
├── README.md
│
├── workflows/
│   ├── lifecycle.md
│   └── multi-agent-execution.md
│
├── execution/
│   ├── task-ledger.md
│   ├── event-log.md
│   └── status.md
│
├── agents/
│   ├── orchestrator.md
│   ├── product.md
│   ├── research.md
│   ├── engineering.md
│   ├── qa.md
│   └── security.md
│
├── artifacts/
│   ├── intent.md
│   ├── ideation.md
│   ├── validation.md
│   ├── requirements.md
│   └── plan.md
│
├── gates/
│   └── human-approval.md
│
├── state/
│   └── project-state.md
│
└── docs/
    ├── V1_BUILD_REPORT.md
    ├── V1_0_1_BUILD_REPORT.md
    └── SKILL_PACKAGING.md
```

---

## Core operating model

CodeFoundry separates **orchestration** from **judgment**.

### System responsibility

The system determines:

- what phase the project is in
- what is missing
- what is uncertain
- what should happen next
- which specialist agents are appropriate
- what evidence should be researched
- what tasks can run in parallel
- what dependencies must be respected
- what artifact should be produced
- whether an artifact is sufficiently complete for the current gate
- what progress should be reported

### Human responsibility

The human determines:

- whether a consequential direction is acceptable
- whether a product decision is approved
- whether risk is acceptable
- whether a release should proceed
- whether an exception should be accepted
- whether the project should continue, change direction, or stop

---

## Human approval gates

Gates are hard boundaries, not ceremonial checkpoints.

A gate can result in:

```text
APPROVED → continue
REJECTED → revise and return
BLOCKED → resolve blocker
ESCALATED → human/legal/security/etc. review
```

CodeFoundry must never treat absence of an explicit approval as approval.

Material changes can invalidate earlier approvals and require affected downstream work to be re-run.

---

## Research and evidence discipline

CodeFoundry distinguishes between:

- verified facts
- user-provided facts
- observations
- assumptions
- inferences
- recommendations
- decisions
- risks

Externally verifiable information should be researched when it can materially affect a decision.

Research evidence is not automatically legal clearance, certification, or approval.

---

## Specialist model

The initial specialist set is intentionally small:

| Role | Primary responsibility |
|---|---|
| Orchestrator | lifecycle control, routing, gates, task graph, next action |
| Product | problem, user, value, scope, requirements |
| Research | evidence, market, competitors, naming, validation |
| Engineering | technical planning and implementation |
| QA | verification, testing, quality evidence |
| Security | security, privacy, threats, risk |

Only required specialists should be activated. Multiple specialists may work concurrently when the dependency graph permits it.

---

## State and coordination

Project state is the authoritative current snapshot.

The task ledger records work ownership and execution state.

The event log records meaningful history.

The human-facing status summarizes current progress.

This separation prevents the conversation itself from becoming the only source of project memory.

---

## Failure, blocking, and re-entry

Failed tasks remain visible. Retries do not erase failure evidence.

The orchestrator must detect or surface:

- dependency blockers
- circular dependencies
- repeated retries without new evidence
- agent-to-agent livelock
- conflicting authoritative writes
- downstream work invalidated by new evidence

When re-entry occurs, affected artifacts and decisions remain in history and affected downstream gates are re-run.

---

## Runtime boundary

Version 1.0.1 defines the multi-agent coordination protocol but does not claim to be a universal agent runtime.

It does not itself provide:

- a hosted workflow engine
- automatic process spawning on every host
- a database-backed runtime
- a dashboard
- authentication
- billing
- distributed infrastructure
- autonomous production deployment

A compatible host/runtime can implement these capabilities around the CodeFoundry contracts.

---

## Version 1.0.1 acceptance target

A host integration must demonstrate:

| Test | Expected |
|---|---|
| Fresh project creates task graph | Pass |
| Independent Product + Research work can run concurrently | Pass |
| Dependent Engineering work waits for upstream outputs | Pass |
| Conflicting writes are serialized | Pass |
| Failed specialist work remains visible | Pass |
| Blocked/waiting work is visible to the human | Pass |
| Human-facing status avoids raw telemetry flooding | Pass |
| Human gate blocks execution | Pass |
| “Build it now” cannot approve an unreviewed technical plan | Pass |
| Material plan changes trigger affected re-approval | Pass |
| Re-entry creates affected downstream work | Pass |
| Circular dependencies are detected | Pass |
| Livelock/retry loops are stopped | Pass |

These are acceptance targets, not claims that the repository alone provides the runtime required to execute them.

---

## How the version should be evaluated

Do not judge CodeFoundry only by whether its documents look good.

Exercise it with a fresh software idea and observe:

### Lifecycle

- Did it know the current stage?
- Did it know what should happen next?
- Did it avoid silently skipping required work?
- Could it move backward when evidence required it?

### Multi-agent execution

- Were independent specialists actually separated by the host?
- Did independent tasks run concurrently?
- Were dependencies respected?
- Were conflicts and failures visible?

### Human control

- Did it stop at meaningful decision points?
- Could a human reject and revise a proposal?
- Was approval evidence recorded?
- Did implementation wait for required technical-plan approval?

### Observability

- Could a human leave the project for 30–40 minutes and understand what happened from the status summary?
- Were meaningful milestones reported?
- Were blocked and waiting states visible?
- Could detailed evidence be inspected without forcing the human to watch it continuously?

### State and artifacts

- Could work resume after interruption?
- Was important context preserved?
- Could the next specialist operate from durable artifacts rather than conversation reconstruction?

The answers determine the next version.

---

## Product feasibility gate

After execution validation, the next major review remains the commercial and product feasibility of CodeFoundry itself.

The review should determine:

- what is actually being sold
- who has the problem
- who uses it
- who pays
- measurable customer value
- competitive alternatives
- differentiation
- product category
- open vs proprietary boundaries
- pricing model
- distribution model
- defensibility
- operating cost
- support burden
- market opportunity
- legal/IP considerations
- willingness to pay
- commercial MVP

Possible outcomes remain:

```text
KEEP
MODIFY
PIVOT
ABANDON
```

---

## Version evolution

The version sequence now intentionally uses **1.0.1** for the multi-agent execution/observability milestone requested for this project.

Future versions should earn their complexity through evidence rather than being predetermined feature promises.

```text
V1.0
Functional lifecycle/control-plane foundation
        ↓
V1.0.1
Multi-agent execution contract + progress observability
        ↓
Future
Reliable runtime + state + validation + governance + integrations
        ↓
Mature production/commercial platform
```

---

## Reference documents

- [`SKILL.md`](SKILL.md) — operational entry point
- [`workflows/lifecycle.md`](workflows/lifecycle.md) — lifecycle and transitions
- [`workflows/multi-agent-execution.md`](workflows/multi-agent-execution.md) — task graph and coordination
- [`execution/task-ledger.md`](execution/task-ledger.md) — task contract
- [`execution/event-log.md`](execution/event-log.md) — event contract
- [`execution/status.md`](execution/status.md) — human-facing progress contract
- [`agents/orchestrator.md`](agents/orchestrator.md) — control role
- [`agents/product.md`](agents/product.md) — product role
- [`agents/research.md`](agents/research.md) — research role
- [`agents/engineering.md`](agents/engineering.md) — engineering role
- [`agents/qa.md`](agents/qa.md) — QA role
- [`agents/security.md`](agents/security.md) — security role
- [`gates/human-approval.md`](gates/human-approval.md) — human gate contract
- [`state/project-state.md`](state/project-state.md) — state contract
- [`artifacts/`](artifacts/) — lifecycle artifact templates
- [`docs/V1_0_1_BUILD_REPORT.md`](docs/V1_0_1_BUILD_REPORT.md) — version 1.0.1 build and acceptance record
- [`docs/V1_BUILD_REPORT.md`](docs/V1_BUILD_REPORT.md) — original V1 implementation record
- [`docs/SKILL_PACKAGING.md`](docs/SKILL_PACKAGING.md) — skill packaging guidance

---

## Design principles

CodeFoundry favors:

- evidence over assumption
- human judgment over silent autonomy
- artifacts over ephemeral conversation
- traceability over guesswork
- risk-based rigor over bureaucracy
- independent specialist work over one-session role simulation
- milestone observability over telemetry flooding
- small working increments over premature architecture
- production behavior over demo behavior
- customer evidence over internal enthusiasm

**Build → Test → Learn → Decide → Evolve.**
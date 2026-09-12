# CodeFoundry

**A generic production SDLC orchestration and control-plane skill.**

CodeFoundry is designed to take a software idea or software objective and guide it through a disciplined lifecycle: discovery, validation, requirements, architecture, implementation, testing, release, deployment, production operations, and continuous improvement.

> **The system decides what needs to happen next. The human decides whether that step is approved.**

---

## Current development milestone

# Ideation Engine V1 — Phase-by-Phase Development

CodeFoundry is currently developing **Ideation Engine V1** on the dedicated `ideation_engine_V.1` branch.

This branch is intentionally isolated from `main`. The purpose is to build, test, challenge, and refine the complete Ideation Engine before merging it into the stable CodeFoundry line.

The Ideation Engine is not a separate lifecycle or a replacement for the CodeFoundry control plane. It is the dedicated ideation execution layer inside the existing lifecycle.

### Ideation Engine V1 goal

Turn a normal user's rough idea into a **validated, decision-ready product initiative** through a guided, beginner-friendly process while CodeFoundry keeps the underlying SDLC complexity internal.

The user should be able to describe an idea naturally without needing to understand product-management or software-engineering terminology.

```text
USER IDEA
   ↓
IDEA INTAKE
   ↓
PROBLEM FRAMING
   ↓
TARGET USER / CONTEXT
   ↓
VALIDATION
   ↓
CONCEPT
   ↓
MARKET / ALTERNATIVES
   ↓
FEASIBILITY
   ↓
MVP SCOPE
   ↓
ADVERSARIAL REVIEW
   ↓
IDEATION DECISION
   ↓
INCEPTION / DOWNSTREAM SDLC
```

The phases are developed incrementally. A later phase must not silently bypass the gates, evidence requirements, or decisions of earlier phases.

---

## Ideation Engine V1 — development status

### Phase 1 — Idea Intake / Understanding

**Current development focus: Phase 1.**

Phase 1 turns an unstructured idea into a faithful structured understanding of what the user is trying to create.

It captures:

- the user's original idea
- interpreted intent
- what the user explicitly has in mind
- intended users when stated
- the problem or need as described by the user
- explicit constraints and exclusions
- assumptions
- unknowns
- clarification questions and answers
- current understanding and confidence
- user-provided research and references
- relevant websites
- GitHub repositories
- documents and PDFs
- screenshots
- apps/products
- notes and other supplied material

### Beginner-friendly interaction

Phase 1 is deliberately conversational.

CodeFoundry should ask only the questions that materially improve its understanding of the idea. A maximum of **three critical clarification questions in an initial round** is the normal guardrail; it is not a rigid questionnaire quota. If an answer reveals a genuinely new ambiguity, another focused round may be appropriate.

The system should avoid making the user operate an SDLC form.

For example:

```text
User:
"I want to build an app like Uber but for home cleaning."

CodeFoundry:
"Got it. Who do you imagine using it most — people
looking for cleaners, cleaning professionals, or both?"
```

The purpose is understanding, not premature product judgment.

### Reference and evidence collection

Phase 1 supports an **optional** prompt such as:

> "Do you have any references you'd like me to look at?"

The user may provide nothing, or may provide websites, GitHub repositories, PDFs, screenshots, apps/products, notes, or other research.

These references are preserved as first-class inputs to the Ideation artifact.

A user-provided reference is treated as **evidence of user interest/context, not automatically as evidence of truth**. Phase 1 does not turn a supplied website into a validated competitor, a supplied document into verified market evidence, or a GitHub repository into a technical recommendation.

Full market, competitor, feasibility, technical, legal, and validation analysis belongs to later ideation phases.

### Prompt methodology integration

Ideation Engine V1 incorporates selected methodology from structured prompt-design approaches where it strengthens Phase 1:

- intent extraction
- identification of critical missing context
- targeted clarification
- limited questioning
- context retention
- explicit constraints
- examples and references
- success/understanding checks
- quality verification

The methodology is adapted to CodeFoundry's product-development lifecycle. It is **not** a separate prompt-generation subsystem.

### Phase 1 flow

```text
RAW IDEA
  ↓
CAPTURE ORIGINAL IDEA
  ↓
EXTRACT INITIAL INTENT
  ↓
IDENTIFY CRITICAL AMBIGUITY
  ↓
ASK FEW HIGH-VALUE QUESTIONS
  ↓
UPDATE UNDERSTANDING
  ↓
REASSESS REMAINING AMBIGUITY
  ↓
OPTIONALLY COLLECT USER REFERENCES
  ↓
BUILD EXISTING IDEATION ARTIFACT
  ↓
QUALITY CHECK
  ↓
PHASE 1 GATE
  ↓
PROBLEM FRAMING
```

### Phase 1 boundary

Phase 1 must **not**:

- decide whether the product is viable
- decide whether it should be built
- perform full market research
- perform full competitor analysis
- define architecture
- choose technology
- create production requirements
- define the MVP
- make final product decisions
- perform full feasibility analysis
- bypass a later approval gate

Phase 1 may collect and preserve information that will be needed by those later activities.

### Phase 1 completion target

Phase 1 is complete when CodeFoundry has:

- preserved the original idea;
- separated user-provided information from inference;
- captured the current understanding of the idea;
- resolved the most important ambiguity that can reasonably be resolved at this stage;
- avoided repetitive or unnecessary questions;
- captured explicit constraints and exclusions;
- preserved user-provided references;
- recorded assumptions and unknowns;
- produced and quality-checked the existing Ideation artifact;
- determined the appropriate Phase 1 outcome;
- respected the existing human gate.

Possible outcomes include:

```text
READY FOR NEXT PHASE
NEEDS CLARIFICATION
BLOCKED
```

---

## Ideation Engine V1 development strategy

The Ideation Engine is being developed **phase by phase**, rather than as one large autonomous system.

```text
Phase 1 — Idea Intake          ← CURRENT
Phase 2 — Problem Framing
Phase 3 — Target User / Context
Phase 4 — Validation
Phase 5 — Concept
Phase 6 — Market / Alternatives
Phase 7 — Feasibility
Phase 8 — MVP Scope
Phase 9 — Adversarial Review
Phase 10 — Ideation Decision
```

Each phase will be:

1. designed against the existing CodeFoundry contracts;
2. implemented in the dedicated development branch;
3. tested independently;
4. subjected to adversarial testing;
5. corrected based on evidence;
6. re-tested before the next phase is considered complete.

The completed Ideation Engine will then undergo final integration testing before it is considered for merge into `main`.

---

## Branch strategy

The Ideation Engine is intentionally isolated during development:

```text
main
 │
 │  Stable CodeFoundry baseline
 │
 └──────────────► ideation_engine_V.1
                       │
                       ├── Phase 1
                       ├── Test
                       ├── Adversarial review
                       ├── Fix
                       ├── Retest
                       │
                       ├── Phase 2
                       ├── Test
                       ├── Fix
                       │
                       └── ...
                              ↓
                       Ideation Engine V1
                              ↓
                         Final QA
                              ↓
                       Integration review
                              ↓
                         Merge to main
```

**No Ideation Engine work is considered part of stable `main` until the completed engine has earned that merge through testing and review.**

---

## Existing CodeFoundry foundation

The Ideation Engine builds on the existing CodeFoundry control-plane foundation rather than replacing it.

The foundation includes:

- explicit lifecycle stages
- durable artifact handoffs
- persistent project-state expectations
- dynamic specialist routing
- research-before-assertion discipline
- human approval gates
- rejection and revision paths
- traceability expectations
- production and post-production lifecycle coverage
- multi-agent execution contracts
- task ownership and dependencies
- event-based progress
- blocked and waiting states
- controlled re-entry

The Ideation Engine therefore extends the existing system instead of introducing a parallel lifecycle.

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

## Human control remains mandatory

The Ideation Engine does not weaken CodeFoundry's existing governance model.

A user saying:

```text
"Build it now."
```

does not automatically approve decisions that require a later human gate.

In particular:

```text
User enthusiasm
      ≠
Technical approval
      ≠
Release approval
      ≠
Production approval
```

The system may continue only when the applicable gate conditions have been satisfied.

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
│   ├── multi-agent-execution.md
│   └── ideation-phase-1.md
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

The CodeFoundry repository defines contracts and operating procedures; it is not itself a universal hosted agent runtime.

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

## Evaluation philosophy

Do not judge CodeFoundry only by whether its documents look good.

The Ideation Engine and the broader lifecycle must be exercised with realistic and adversarial scenarios.

Testing should verify that CodeFoundry:

- understands a normal user's rough idea;
- asks useful questions without overwhelming the user;
- preserves context across turns;
- does not repeatedly ask already answered questions;
- distinguishes user statements from inference;
- preserves user-provided references;
- does not prematurely convert references into conclusions;
- respects phase boundaries;
- produces durable artifacts;
- stops at required gates;
- remains traceable when work is rejected, revised, blocked, or re-entered.

The answers determine the next version.

---

## Future version evolution

Future CodeFoundry versions should earn their complexity through evidence rather than being predetermined feature promises.

```text
V1.0
Functional lifecycle/control-plane foundation
        ↓
V1.0.1
Multi-agent execution contract + progress observability
        ↓
Ideation Engine V1
Dedicated phase-by-phase ideation execution
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
- [`workflows/ideation-phase-1.md`](workflows/ideation-phase-1.md) — Phase 1 execution procedure
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
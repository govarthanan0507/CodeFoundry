# CodeFoundry

**A generic production SDLC orchestration and control-plane skill.**

CodeFoundry is designed to take a software idea or software objective and guide it through a disciplined lifecycle: discovery, validation, requirements, architecture, implementation, testing, release, deployment, production operations, and continuous improvement.

> **The system decides what needs to happen next. The human decides whether that step is approved.**

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

## V1 status

**V1 foundation is implemented.**

V1 is deliberately lightweight. It is not a SaaS platform, dashboard, distributed orchestration engine, billing system, or enterprise product.

V1 establishes the operational contract that a host agent can follow:

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

The goal of V1 is to prove the control loop before adding infrastructure.

---

## Core operating model

CodeFoundry separates **orchestration** from **judgment**.

### System responsibility

The system determines:

- what phase the project is in
- what is missing
- what is uncertain
- what should happen next
- which specialist is appropriate
- what evidence should be researched
- which artifact should be produced
- whether an artifact is sufficiently complete for the current gate

### Human responsibility

The human determines:

- whether a consequential direction is acceptable
- whether a product decision is approved
- whether risk is acceptable
- whether a release should proceed
- whether an exception should be accepted
- whether the project should continue, change direction, or stop

---

## V1 repository structure

```text
CodeFoundry/
│
├── SKILL.md
├── README.md
│
├── workflows/
│   └── lifecycle.md
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
└── state/
    └── project-state.md
```

The structure is intentionally small. It is expected to change as V1 is exercised and evidence shows what should be kept, removed, or expanded.

---

## Lifecycle

The V1 lifecycle is:

1. Idea
2. Problem
3. Target User
4. Validation
5. Concept
6. Naming
7. Name Validation
8. Market / Competitor Research
9. Feasibility
10. Requirements
11. Product Definition
12. Architecture
13. Security / Privacy
14. Technical Plan
15. Implementation
16. Testing
17. Review
18. Integration
19. Staging
20. Release Readiness
21. Deployment
22. Production
23. Monitoring
24. Incident / Improvement
25. Next Iteration

Not every project needs identical depth at every stage. Risk determines how much rigor is appropriate.

---

## Artifact-driven workflow

CodeFoundry uses durable artifacts as lifecycle memory.

A simplified handoff looks like:

```text
intent.md
   ↓
ideation.md
   ↓
validation.md
   ↓
requirements.md
   ↓
plan.md
   ↓
implementation + tests
   ↓
release evidence
   ↓
production evidence
   ↓
incident / improvement record
```

The important property is not the filenames. The important property is that meaningful decisions and evidence survive beyond the immediate conversation.

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

---

## Research and evidence discipline

CodeFoundry distinguishes between:

- verified facts
- user-provided facts
- assumptions
- inferences
- recommendations
- decisions
- risks

Externally verifiable information should be researched when it can materially affect a decision.

For example, naming research can examine existing products, companies, repositories, domains, package registries, app stores, and obvious language/geographic conflicts. A research result is not the same as legal clearance.

---

## Specialist model

V1 does not require dozens of permanently active agents.

Specialists are activated according to need.

| Role | Primary responsibility |
|---|---|
| Orchestrator | lifecycle control, routing, gates, next action |
| Product | problem, user, value, scope, requirements |
| Research | evidence, market, competitors, naming, validation |
| Engineering | technical planning and implementation concerns |
| QA | verification, testing, quality evidence |
| Security | security, privacy, threats, risk |

Later versions may add architecture, release, operations, incident, documentation, compliance, or domain-specific specialists.

---

## What V1 deliberately does not include

V1 does not attempt to provide:

- a web dashboard
- a hosted SaaS service
- user authentication
- billing
- distributed agent infrastructure
- a database-backed orchestration engine
- enterprise identity integration
- every possible SDLC template
- dozens of specialist roles
- automatic legal approval
- automatic commercial validation
- autonomous production deployment

Those are potential future capabilities, not V1 requirements.

---

## How V1 should be evaluated

Do not judge V1 only by whether the files look good.

Exercise the lifecycle with real project work and ask:

### Lifecycle

- Did it know the current stage?
- Did it know what should happen next?
- Did it avoid skipping required stages?
- Could it move backward when evidence required it?

### Human control

- Did it stop at meaningful decision points?
- Could a human reject and revise a proposal?
- Was approval evidence recorded?

### Research

- Did it identify important unknowns?
- Did it research externally verifiable claims?
- Did it distinguish facts from assumptions?

### Artifacts

- Were the artifacts useful?
- Could the next stage operate from them?
- Was traceability preserved?

### State

- Could work resume after interruption?
- Was important context preserved?

### Routing

- Were the correct specialists activated?
- Were unnecessary specialists avoided?

### Product value

- Did the lifecycle prevent an expensive mistake?
- Did it reduce ambiguity?
- Did it improve delivery discipline?

The answers determine V2.

---

## First major post-V1 gate: product feasibility

After V1 is exercised, the first major review is not simply a feature review.

It is a **commercial and product feasibility review of CodeFoundry itself**.

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

Possible outcomes are deliberately:

```text
KEEP
MODIFY
PIVOT
ABANDON
```

The project should be willing to accept any of these outcomes based on evidence.

---

## V1 → VN direction

The expected evolution is:

```text
V1
Functional lifecycle proof
        ↓
V2
Reliable state + better artifacts
        ↓
V3
Structured orchestration + validation
        ↓
V4
Governance + integrations
        ↓
V5+
Productization
        ↓
VN
Mature production/commercial platform
```

This is a direction, not a fixed feature promise. Each version should earn its complexity through evidence from the previous version.

---

## Design principles

CodeFoundry favors:

- evidence over assumption
- human judgment over silent autonomy
- artifacts over ephemeral conversation
- traceability over guesswork
- risk-based rigor over bureaucracy
- small working increments over premature architecture
- production behavior over demo behavior
- customer evidence over internal enthusiasm

---

## V1 reference documents

- [`SKILL.md`](SKILL.md) — operational entry point
- [`workflows/lifecycle.md`](workflows/lifecycle.md) — lifecycle and transitions
- [`agents/orchestrator.md`](agents/orchestrator.md) — control role
- [`agents/product.md`](agents/product.md) — product role
- [`agents/research.md`](agents/research.md) — research role
- [`agents/engineering.md`](agents/engineering.md) — engineering role
- [`agents/qa.md`](agents/qa.md) — QA role
- [`agents/security.md`](agents/security.md) — security role
- [`gates/human-approval.md`](gates/human-approval.md) — human gate contract
- [`state/project-state.md`](state/project-state.md) — state contract
- [`artifacts/`](artifacts/) — V1 artifact templates
- [`docs/V1_BUILD_REPORT.md`](docs/V1_BUILD_REPORT.md) — detailed V1 implementation record

---

## Long-term vision

The long-term direction is not simply a system that generates code.

It is a reusable production engineering control system that can take software intent, coordinate the necessary lifecycle activities, preserve decisions and evidence, enforce appropriate gates, and guide work into production operations and the next iteration.

**Build → Test → Learn → Decide → Evolve.**
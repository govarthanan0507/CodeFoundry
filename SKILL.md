# CodeFoundry — Production SDLC Orchestrator

## Purpose

CodeFoundry is a generic, artifact-driven SDLC orchestration skill. It takes a software idea or software objective and drives it through a controlled lifecycle from discovery to production and continuous improvement.

## Core rule

**The system decides what needs to happen next. The human decides whether that step is approved.**

The system may research, analyze, plan, generate artifacts, implement, test, review, and recommend. It must not silently bypass mandatory human gates or turn unverified assumptions into project facts.

## Automatic activation

When a user provides a new software idea, objective, or project request:

1. Determine whether this is a new project or an existing project.
2. If it is new, initialize lifecycle state automatically.
3. Start at IDEATION unless accepted artifacts already establish a later stage.
4. Identify facts, assumptions, unknowns, risks, and decisions required.
5. Select only the specialist roles required for the current work.
6. Research externally verifiable questions instead of guessing.
7. Produce a durable artifact for meaningful work.
8. Validate the artifact.
9. Evaluate the applicable gate.
10. Stop for human approval whenever the gate requires judgment.
11. Record the decision and update project state.
12. Determine the next action.

## Lifecycle

IDEA → PROBLEM → TARGET USER → VALIDATION → CONCEPT → NAMING → NAME VALIDATION → MARKET/COMPETITOR RESEARCH → FEASIBILITY → REQUIREMENTS → PRODUCT DEFINITION → ARCHITECTURE → SECURITY/PRIVACY → TECHNICAL PLAN → IMPLEMENTATION → TESTING → REVIEW → INTEGRATION → STAGING → RELEASE READINESS → DEPLOYMENT → PRODUCTION → MONITORING → INCIDENT/IMPROVEMENT → NEXT ITERATION

The lifecycle is a directed graph, not an irreversible linear pipeline. Downstream evidence may require a controlled return to an earlier stage.

## State

Maintain durable project state containing at least:

- current phase
- current state
- risk level
- active specialist roles
- completed and pending artifacts
- pending, approved, and rejected decisions
- assumptions
- unresolved risks
- failed gates
- next action
- traceability information

Use `state/project-state.md` as the V1 state contract.

## Artifact rule

Meaningful stages produce durable artifacts. The next stage reads accepted artifacts from the previous stage rather than relying only on conversational memory.

V1 artifacts:

- `intent.md`
- `ideation.md`
- `validation.md`
- `requirements.md`
- `plan.md`

Later versions may add architecture, security, test, release, incident, postmortem, and decision artifacts.

## Evidence rule

Every material claim should be classified where relevant as:

- Verified fact
- User-provided fact
- Assumption
- Inference
- Recommendation
- Decision
- Risk

External facts that can materially affect a decision should be researched.

## Specialist routing

Do not activate every specialist for every project. Select specialists according to the current phase and risk.

V1 roles:

- Orchestrator — lifecycle control and next-action selection
- Product — problem, users, product boundary, requirements
- Research — external evidence, market, competitor, naming and validation research
- Engineering — technical planning and implementation concerns
- QA — verification, test strategy and quality gates
- Security — security, privacy, threat and risk review

## Human gates

Mandatory gates are hard boundaries. If a required approval is absent, the system stops.

A rejection means revision is required. It does not mean approval.

Never:

- silently skip a gate
- fabricate evidence
- claim legal clearance without appropriate legal evidence
- claim market validation without validation evidence
- hide failed tests or security findings
- overwrite a human decision without an explicit new decision
- pretend an artifact exists when it does not

## Completion

V1 is complete when the lifecycle control loop is represented, state and artifacts are defined, human gates are defined, specialist routing is defined, and the repository provides a usable generic operational contract. V1 does not attempt to implement a full hosted platform or enterprise control plane.

## References

Read `workflows/lifecycle.md` for stage behavior, `gates/human-approval.md` for approval rules, the role files under `agents/`, and the templates under `artifacts/` and `state/` as needed.
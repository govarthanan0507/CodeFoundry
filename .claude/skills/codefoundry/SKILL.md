---
name: codefoundry
description: >
  Applies the CodeFoundry production SDLC control process to software work,
  including lifecycle routing, evidence discipline, durable artifacts,
  specialist coordination, human approval gates, risk management, and
  traceability. Use for software projects from idea through production and
  continuous improvement.
---

# CodeFoundry repository skill adapter

This is the repository-discovery entry point for CodeFoundry.

The canonical operational contract is the repository-root `SKILL.md`. Read it first. Then read only the supporting files required for the current lifecycle stage:

- `../../workflows/lifecycle.md`
- `../../gates/human-approval.md`
- `../../agents/*.md`
- `../../artifacts/*.md`
- `../../state/project-state.md`

Follow the canonical contract exactly. Do not create a second or conflicting lifecycle model here.

## Required behavior

- Determine the current phase from durable project state and accepted artifacts.
- Determine the next valid action rather than waiting for the user to specify every lifecycle step.
- Preserve facts, assumptions, unknowns, risks, decisions, approvals, rejections, and superseded decisions separately.
- Research material external claims instead of guessing.
- Create durable artifacts for meaningful work.
- Never infer human approval from silence.
- Never silently skip a mandatory gate.
- Stop at required human approval boundaries.
- Re-enter earlier phases when later evidence materially invalidates earlier work.
- Keep project state synchronized with reality.

User instructions remain authoritative. When a user changes a consequential direction, record the resulting decision and update lifecycle state.

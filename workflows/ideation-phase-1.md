# CodeFoundry — Ideation Phase 1: Idea Intake

## 1. Purpose

This document defines the execution procedure for **Phase 1 of the existing Ideation lifecycle**.

It is not a new lifecycle, subsystem, research engine, or alternate artifact model. It operationalizes the existing ideation stage using the existing `artifacts/ideation.md` artifact and the existing human gate model.

## 2. Phase objective

Turn a raw human idea into a faithful, structured understanding of what the user is trying to create, while preserving the user's own context, constraints, research, and optional references.

The experience should feel simple to a beginner. CodeFoundry absorbs the SDLC complexity internally.

## 3. User experience principle

The user should be able to explain an idea naturally.

Do not expose unnecessary terms such as requirements engineering, architecture, task graphs, ADRs, or lifecycle control during Phase 1.

Use plain-language questions such as:

- Who do you imagine using this?
- What problem would this help them with?
- What made you think of this idea?
- Have you seen anything similar?
- Do you have any websites, GitHub repositories, documents, screenshots, apps, or notes you want me to look at?

The reference question is optional, not a mandatory questionnaire item.

## 4. Phase 1 flow

```text
RAW IDEA
  ↓
CAPTURE ORIGINAL IDEA
  ↓
EXTRACT INITIAL INTENT
  ↓
CHECK FOR MATERIAL AMBIGUITY
  ↓
ASK FEW HIGH-VALUE QUESTIONS
  ↓
UPDATE UNDERSTANDING
  ↓
REASSESS AMBIGUITY
  ├── material ambiguity remains → focused clarification
  └── sufficient understanding → continue
  ↓
OPTIONALLY COLLECT USER-PROVIDED REFERENCES
  ↓
BUILD EXISTING IDEATION ARTIFACT
  ↓
QUALITY CHECK
  ↓
PHASE 1 GATE
  ↓
PROBLEM FRAMING
```

## 5. Step 1 — Capture the raw idea

Record the user's original idea as faithfully as possible.

Rules:

- Do not improve the idea silently.
- Do not convert it into a PRD.
- Do not replace the user's wording with assumptions.
- Preserve important user language that may affect later interpretation.

## 6. Step 2 — Extract initial intent

Identify what CodeFoundry currently believes the user means.

At minimum, consider:

- intended task or outcome,
- type of product/system if apparent,
- intended users if stated,
- problem or need if stated,
- desired experience or core interaction if stated,
- constraints explicitly mentioned,
- examples or references mentioned.

Clearly separate:

```text
USER-PROVIDED

from

CODEFOUNDRY INFERENCE
```

Do not treat an inference as a confirmed requirement or decision.

## 7. Step 3 — Detect material ambiguity

Ask whether the current understanding is sufficient to represent the user's idea faithfully.

Only material ambiguity matters.

Examples of material ambiguity:

- two plausible interpretations would lead to substantially different products,
- the intended user is unclear and that changes the basic idea,
- the core problem is unclear,
- an explicit constraint conflicts with the apparent intent.

Do not ask about details that belong to later phases merely because they are unknown.

## 8. Step 4 — Ask targeted questions

Use the following discipline:

1. Ask the highest-value question first.
2. Ask only what can materially improve the current understanding.
3. Use **three critical questions as the normal upper bound for the initial clarification round**.
4. After answers arrive, reassess rather than automatically asking three more.
5. Ask another focused question only if a newly revealed material ambiguity remains.
6. Never repeat a question already answered or explicitly rejected.

This is adapted from targeted intent-clarification methodology: the goal is better understanding, not completion of a questionnaire.

### Question selection heuristic

Prefer a question when its answer:

- changes the likely interpretation of the idea,
- resolves an important ambiguity,
- establishes an explicit user constraint,
- identifies the intended user/problem,
- explains why a supplied reference matters.

Avoid a question when its answer only fills in details that can safely wait for a later phase.

## 9. Step 5 — Preserve context

After every clarification round, update the Phase 1 context/memory block.

Preserve:

- original idea,
- confirmed information,
- user corrections,
- rejected interpretations,
- important constraints,
- current understanding,
- unresolved questions,
- references supplied by the user.

The system must not make the user repeat information already established.

## 10. Step 6 — Optional reference collection

Near the end of Phase 1, optionally ask whether the user has anything they want CodeFoundry to look at.

Supported reference types:

- Website
- GitHub repository
- Document / PDF
- Screenshot
- App / product
- Notes / research
- Other relevant material

The user may provide nothing. That is a valid outcome.

### Reference record

Each supplied reference should capture:

- reference ID,
- source type,
- source/location,
- user's description,
- intended relevance,
- analysis status.

Example:

```text
REF-01
Type: GitHub repository
Source: <repository>
User's description: "I like how this handles project setup."
Intended relevance: Project setup experience
Analysis status: NOT YET ANALYZED
```

### Reference evidence rule

User-provided references are evidence of user interest or context, not proof of truth.

For example, if the user says:

> "I want something exactly like this website."

Phase 1 records the website and the user's stated intent. It must not conclude that the website is the correct competitor, that its model is viable, that the feature set is required, or that its technology should be copied.

Those analyses belong to later stages.

## 11. GitHub references

GitHub is a normal reference source within the existing reference model.

Do not create:

- a GitHub-specific subsystem,
- a GitHub research engine,
- a GitHub-only artifact,
- a separate GitHub lifecycle.

A GitHub repository is simply another user-provided reference that Phase 1 can preserve for later analysis.

## 12. Phase 1 boundaries

Phase 1 may:

- capture the idea,
- understand intent,
- identify ambiguity,
- ask targeted questions,
- preserve context,
- capture explicit constraints,
- collect user-provided references,
- preserve user-supplied research and notes,
- identify assumptions and unknowns,
- record understanding confidence,
- build and validate `artifacts/ideation.md`.

Phase 1 must not:

- validate market demand,
- perform full competitor research,
- perform full market research,
- determine feasibility,
- select technology,
- design architecture,
- define detailed requirements,
- define MVP scope,
- decide whether to build,
- convert references into requirements,
- claim supplied references are verified evidence,
- bypass the existing human gate.

## 13. Specialist routing

Default Phase 1 routing:

```text
ORCHESTRATOR
     │
     ├── PRODUCT (when interpretation of user/problem/value needs help)
     │
     └── RESEARCH (only for preservation/identification of supplied material
                   or an explicitly required Phase 1 evidence task)
```

Engineering, QA, and Security should not be activated simply because a new idea exists. They become relevant when later lifecycle stages or material risks require them.

The orchestrator remains the only role allowed to change lifecycle phase or declare the gate passed.

## 14. Existing artifact

All Phase 1 information is recorded in the existing:

`artifacts/ideation.md`

Do not create a parallel Idea Intake artifact.

The artifact must be understandable without reconstructing the conversation.

## 15. Quality check

Before Phase 1 gate submission, verify:

- original idea is preserved,
- current understanding is faithful,
- user-provided facts are separated from inference,
- material ambiguity is surfaced,
- questions were targeted and non-redundant,
- context was retained,
- explicit constraints and exclusions are preserved,
- optional references are preserved as first-class records,
- GitHub references use the same model as other references,
- user-supplied research is preserved without automatic verification,
- no downstream analysis has been smuggled into Phase 1,
- artifact is sufficient for Problem Framing.

If the quality check fails, remain in Phase 1 and revise the artifact.

## 16. Completion criteria

Phase 1 is complete only when:

1. The original idea is captured.
2. CodeFoundry's current understanding is explicit.
3. Important ambiguity has been addressed or intentionally carried forward.
4. Important assumptions and unknowns are visible.
5. Explicit constraints are preserved.
6. User-provided references are preserved, if any.
7. The artifact passes the Phase 1 quality check.
8. The required human gate is satisfied.
9. Project state records the outcome and next action.

## 17. Gate behavior

The existing human approval model remains authoritative.

Phase 1 must stop when the applicable gate requires human judgment and approval has not been given.

A user saying:

> "Build it now."

does not bypass a later technical-plan approval gate.

Phase 1 approval means the current idea intake is accepted as the basis for moving into the next lifecycle stage. It does not approve architecture, implementation, feasibility, market conclusions, or production deployment.

## 18. Next stage

On successful Phase 1 completion:

```text
IDEATION — PHASE 1: IDEA INTAKE
              ↓
PROBLEM FRAMING
```

The accepted Phase 1 artifact becomes an upstream input for the next stage. Later stages may challenge its assumptions and trigger controlled re-entry when new evidence materially changes the understanding.

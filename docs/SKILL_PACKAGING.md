# CodeFoundry Skill Packaging

## Purpose

CodeFoundry is packaged as a portable Agent Skill using a canonical root `SKILL.md` plus supporting lifecycle resources.

The same canonical skill content can be uploaded to skill systems that accept a directory or ZIP containing `SKILL.md` and supporting files.

## Portable package

The portable package root is:

```text
CodeFoundry/
├── SKILL.md
├── workflows/
├── agents/
├── artifacts/
├── gates/
└── state/
```

`SKILL.md` contains the skill metadata and operational contract. Supporting files are loaded progressively as needed.

## Repository discovery adapter

For repository-based skill discovery, CodeFoundry also provides:

```text
.claude/skills/codefoundry/SKILL.md
```

This adapter points back to the canonical root contract instead of maintaining a second lifecycle implementation.

## Design rule

Do not create separate lifecycle logic for different hosts. Platform-specific wrappers may describe how a host discovers or installs the skill, but the lifecycle, state model, artifacts, evidence rules, specialist model, and human gates remain canonical and vendor-neutral.

## OpenAI-compatible packaging

The root package is suitable for skill upload because it contains a top-level `SKILL.md` with YAML frontmatter containing `name` and `description` and all supporting resources underneath the same package root.

## Repository-based discovery

The `.claude/skills/codefoundry/SKILL.md` adapter exists for repository-based discovery layouts that require a skill directory under `.claude/skills/`.

## Validation checklist

Before releasing a skill package:

- [ ] `SKILL.md` exists at package root
- [ ] YAML frontmatter is valid
- [ ] skill name is lowercase and hyphen-safe
- [ ] description explains both capability and activation context
- [ ] all referenced supporting files exist
- [ ] no host-specific lifecycle logic conflicts with the canonical contract
- [ ] no secrets or credentials are included
- [ ] no generated project state is accidentally packaged
- [ ] skill can be used without relying on hidden conversation history
- [ ] human approval rules remain explicit
- [ ] evidence rules remain explicit
- [ ] rejected and superseded decisions remain preservable

## Installation and testing

Use the platform's current skill installation/upload mechanism to install the package. Then test the same fresh software idea against the package in each target host.

A successful portability test should demonstrate that the host can:

1. discover the skill
2. load the canonical contract
3. initialize project state
4. identify unknowns and assumptions
5. route appropriate specialists
6. create durable artifacts
7. research material external claims
8. stop at human gates
9. record decisions
10. determine the next action
11. preserve traceability across interruption and re-entry

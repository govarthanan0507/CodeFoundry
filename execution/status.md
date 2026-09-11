# CodeFoundry Version 1.0.1 — Human Progress Status

## Purpose

The status view gives the human a concise understanding of project progress without requiring them to watch agent commands or tool telemetry.

## Required sections

```text
CODEFOUNDRY
Project: <name>
Phase: <phase>
Progress: <status>

CURRENTLY WORKING
🟢 <agent> — <meaningful activity>
⏳ <agent> — waiting for <dependency>
🔴 <agent> — blocked by <reason>

LAST COMPLETED
✓ <milestone>
✓ <milestone>

RISKS
⚠ <risk or None>

NEXT GATE
🔴 <gate or None>

NEXT ACTION
<one clear action>
```

## Update policy

Update the human-facing status when a material milestone occurs, including:

- phase transition
- specialist activation
- task completion/failure
- blocker discovery/resolution
- artifact completion
- gate submission or decision
- material risk change
- re-entry
- release/deployment milestone

Do not flood the human with individual shell commands, file-edit notifications, timers, or repetitive internal traces.

## Progress calculation

Progress must be labeled as approximate unless the lifecycle has a deterministic measurable completion model. Never manufacture a precise percentage from weak evidence.

A useful status should answer:

1. Where are we?
2. What is happening now?
3. What finished?
4. What is blocked or waiting?
5. What risks matter?
6. What decision or action is next?

## Drill-down boundary

Detailed execution telemetry may be retained separately for debugging and audit. The human status should link or identify the relevant evidence without making raw telemetry the primary experience.

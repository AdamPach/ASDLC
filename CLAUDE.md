# ASDLC (Agentic Software Development Lifecycle)

ASDLC is a stateful development environment for collaborating with AI across the software development lifecycle. This repository develops it. `ASDLC.md` is the product: it guides AI in projects that adopt ASDLC.

## Collaboration

Applies to every task in this repository.

- Always: understand my intent before proposing solutions.
- When reviewing a draft: check for contradictions, missing assumptions, and blind spots.
- When a draft needs changes: suggest concrete changes; edit only when I ask.
- When an idea is weak: challenge it and offer alternatives.
- When uncertainty affects the approach: ask focused questions.
- When writing any file in this repository:
  - Describe precisely; do not use examples.
  - State when each statement or rule applies, including when it always applies.

## ASDLC.md Guardrails

Applies whenever ASDLC.md is created or changed.

- Max 100 lines.
- Contains only:
  - a short guide on how to use ASDLC,
  - a document map (where project knowledge is stored),
  - a skill map (what each skill does and when AI should invoke it).
- Project-agnostic: no references to this repository or its history.

## Skills Folder

Applies whenever a skill in `skills/` is created, moved, or installed.

- Always: each skill lives at `skills/<group>/<skill-name>/`, and the folder name equals the skill's `name:` field.
- Group folders exist only in this repository. When a skill is installed, copy its folder flat into the target `skills/` folder, because Claude Code discovers skills only one level deep.
- Groups:
  - `feature/`: skills that take a feature from product request to implementation plan.
  - `lifecycle-updates/`: skills AI invokes automatically to keep documents current during the lifecycle.
  - `shared/`: skills other skills use as building blocks.
  - `draft/`: unfinished skills of any group.
- When a skill is created: place it in `draft/`.
- When I declare a skill finished: move it from `draft/` into the group that matches its purpose.

## Skill Versioning

Applies whenever a skill in `skills/` is created or changed.

- Always: a skill's version is stored in its `metadata.version` field as three non-negative integers separated by dots: release, structure, change.
- Release (first number): increment only when I declare a release.
- Structure (second number): increment when a change alters how the skill operates: its steps, inputs, outputs, or the documents it reads or writes.
- Change (third number): increment when a change alters the skill's files without altering how it operates.
- When a number is incremented: reset every number to its right to 0.
- When a skill is created: set its version to `0.0.1`.
- When a task changes a skill: increment its version once for the whole task, at the highest level any change in that task requires.

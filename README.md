# ASDLC

## Installation

Applies when a project adopts ASDLC.

1. Copy `ASDLC.md` into the project root.
2. Copy each skill folder flat into the agent's skills folder, without its group folder. For Claude Code, the skills folder is `.claude/skills/`.
3. Add the ASDLC instruction to the file the agent loads at session start:
   - When the agent is Claude Code: add it to `CLAUDE.md`. The `@ASDLC.md` line imports the file, so its contents are loaded at every session start.

     ```markdown
     ## ASDLC

     Applies to every session in this project.

     @ASDLC.md

     - Always: follow the instructions in `ASDLC.md`, imported above; never edit it.
     - When `ASDLC.md` and this file give conflicting instructions: ask the developer which one applies.
     ```

   - When the agent reads `AGENTS.md`: add it to `AGENTS.md`. `AGENTS.md` has no import syntax, so the agent loads `ASDLC.md` only by following this instruction.

     ```markdown
     ## ASDLC

     Applies to every session in this project.

     - At the start of every session, before any other action: read `ASDLC.md` in the project root and follow its instructions.
     - Always: treat `ASDLC.md` as read-only; never edit it.
     - When `ASDLC.md` and this file give conflicting instructions: ask the developer which one applies.
     ```

   - When the project has both files: add the `CLAUDE.md` version to `CLAUDE.md` and the `AGENTS.md` version to `AGENTS.md`.

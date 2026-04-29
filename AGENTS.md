# AGENTS.md

This is the canonical operating guide for KnowledgeHub agents and human collaborators.

## Project Definition

KnowledgeHub(KH) is not a general project management system. It is a decision-support hub for capturing operator inputs, routing them to the right project context, surfacing decisions, and tracking only the minimum state needed for oversight.

## Core Roles

```text
Capture  - collect thoughts, notes, external inputs, and unresolved signals
Route    - connect inputs to projects, tasks, documents, or decision points
Surface  - show what the operator needs to judge now
Track    - keep minimal visibility on open work, blockers, and important changes
```

## Current Managed Projects

- EOB
- Cafe_ops
- KS / KnowledgeStorage
- Warship

KS is one managed project inside KH. It is not the parent of KH. KS has a special role as a knowledge-storage project because finalized outputs from other projects may be promoted into KS.

## Operating Principles

- Do not turn KH into a heavy PM system.
- Do not force all projects to share detailed management fields.
- Keep common project tracking minimal.
- Put project-specific detail inside each Project Profile.
- Treat Operator Inbox as a capture and anti-forgetting tool.
- Treat Project Creation Pipeline as the setup process for turning ideas into manageable projects.
- Prefer links and references over duplicated content.
- When uncertain, preserve the decision point instead of inventing policy.

## Reference Priority

Read these documents before non-trivial structural or operating changes:

1. `README.md`
2. `_Setup/01_Design/KH-Overview-2026-04-29.md`
3. Relevant area README under `_Hub-Setup/`, `_Operator/`, `_Project-Creation/`, `_Project-Registry/`, or `_Project-Profiles/`

## Write Policy

- Structural changes should update the relevant README or design note.
- Project-specific rules belong in `_Project-Profiles/`.
- Temporary thoughts belong in `_Operator/Inbox.md` or a later inbox tool.
- Do not duplicate long operating policy in tool-specific files such as `CLAUDE.md`.

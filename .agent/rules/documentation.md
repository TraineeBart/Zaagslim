---
description: Context Management and Session Protocol (The Memory System)
trigger: always_on
---

# Rules: Documentation & Context

**Goal**: Maintain a unbroken chain of project history in `.context/`.

## 1. The Single Source of Truth

The `.context/` directory is your external brain.
*   `STATUS.md`: The "Now". Current work, roadmap, known issues. **Max ~80 lines.**
*   `CHANGELOG.md`: The "Done". Completed items, archived from STATUS.md.
*   `DECISIONS.md`: The "Why". Architectural logs.
*   `PROJECT.md`: The "What". High-level goals.
*   `CODEBASE_MAP.md`: The "How". Auto-generated map of all modules, classes, and functions.

## 2. Session Protocol (MANDATORY)

### Start of Session (Boot Sequence)
1.  **Read** `.context/STATUS.md`.
2.  **Read** `.context/CODEBASE_MAP.md` (for symbol/function awareness).
3.  **Read** `.context/PROJECT.md` (if needing big picture).
4.  **Check** recent `DECISIONS.md`.
5.  **Session Contract** — present to user for alignment before any work:
    ```
    🎯 Doel: [1 feature/topic]
    📦 Deliverables: [concrete output]
    🚫 Niet in scope: [explicitly excluded]
    ⏱ Geschatte effort: [sessions/hours]
    ```
6.  **Ack**: "Context geladen. Huidige fase: [X]. Sessie-doel: [Y]."

### End of Session (Shutdown Sequence)
1.  **Update** `.context/STATUS.md`:
    *   Move tasks from `[ ]` to `[x]`.
    *   Add new tasks found during work.
    *   Update "Current Phase" if changed.
    *   **Archive**: Move `[x]` items to `.context/CHANGELOG.md` (newest first). Keep STATUS.md under ~80 lines.
2.  **Log Decisions**:
    *   Did you change a library? -> `DECISIONS.md`.
    *   Did you change the DB schema? -> `DECISIONS.md`.
3.  **Regenerate Codebase Map** (if files were added, renamed, or deleted).
4.  **Handover** — present to user as paste-ready message for the next session:
    ```
    📋 Sessie: [onderwerp]
    ✅ Gedaan: [key deliverables, concrete]
    ⚠️ Open: [unfinished items, blockers, known issues]
    🔜 Volgende sessie: [suggested next step]
    📊 Stats: [tests passing] | [coverage] | [ruff status]
    ```

## 3. Artifacts (`.ai/artifacts/`)

Use artifacts for broad communication:
*   `implementation_plan.md`: For planning features.
*   `analysis_report.md`: For deep dives.
*   `task.md`: For tracking complex multi-step execution.

---
description: Systematic bug fixing using the Scientific Method
---

# Workflow: Bugfix (The Scientific Method)

Use this when fixing a bug. Do not guess.

## Phase 1: Diagnosis

1.  **Reproduction**
    *   Create a reproduction script or a failing test case in `tests/`.
    *   *Goal*: See it fail RED.
    *   If you cannot reproduce it, do not fix it. Ask for more info.

2.  **Hypothesis**
    *   State your hypothesis: "I believe X is failing because Y state is corrupt."
    *   Verify this hypothesis with logs or debugger (print statements).

## Phase 2: The Fix

1.  **Implement Fix**
    *   Apply the minimal change required.
    *   Do not "drive-by refactor" unrelated code.

2.  **Verification**
    *   Run the reproduction test -> Must be GREEN.
    *   Run the full suite -> Ensure NO REGRESSIONS.

## Phase 3: Post-Mortem

1.  **Prevention**
    *   "Could this happen elsewhere?"
    *   "Do we need a better guardrail?"

2.  **Documentation**
    *   Update `.context/STATUS.md`.
    *   Commit with `fix: ...`.

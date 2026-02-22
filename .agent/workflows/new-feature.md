---
description: End-to-end workflow for building new features (Chain of Thought)
---

# Workflow: New Feature (Chain of Thought)

Use this workflow for ANY new functionality. Do not skip steps.

## Phase 1: Thinking (System 2)

1.  **Analysis**
    *   Read `.context/STATUS.md` and `.context/PROJECT.md` to ground yourself.
    *   Read `.context/DECISIONS.md` to ensure architectural alignment.
    *   *Self-Correction*: "Does this feature duplicate existing logic? Is it consistent with the project philosophy?"

2.  **Definition of Done**
    *   Write 3 User Scenarios (Given/When/Then).
    *   Get User Approval on these scenarios.

3.  **Planning**
    *   Create `implementation_plan.md` (Artifact).
    *   List every file to be touched.
    *   Define the data flow.
    *   **STOP**: Request User Review.

## Phase 2: Implementation (Iterative)

*Execute this loop for each layer (Data -> Repo -> Service -> API):*

1.  **Write Tests First (or Simultaneously)**
    *   Create the test file.
    *   Write the test case (Red).

2.  **Implement Code**
    *   Write the code to pass the test (Green).
    *   Ensure type hints and docstrings are present.

3.  **Refactor**
    *   Check file size (<300 lines).
    *   Check function size (<30 lines).

## Phase 3: Adversarial Review (The Red Team)

*You must now critique your own work.*

1.  **Automated Checks**
    *   Run: `pytest --cov=src` -> Must be > 80%.
    *   Run: `ruff check src/` -> Must be clean.

2.  **Manual Audit (Self-Correction)**
    *   "Did I update `.context/DATA.md` if I changed the schema?"
    *   "Did I add a new dependency? If so, is it in `STACK.md`?"

## Phase 4: Delivery

1.  **Documentation**
    *   Update `.context/STATUS.md` (Mark as Done).
    *   Update `.context/DECISIONS.md` (Log key choices).
2.  **Commit**
    *   Suggest a conventional commit message (`feat: ...`).
3.  **Handover**
    *   Present a concise summary to the user.

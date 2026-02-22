---
description: Code and Architecture Standards (The Law)
trigger: always_on
---

# Standards: The Law

These are the non-negotiable standards for the project.

## 1. Python Standards (Strict)

*   **Type Hints**: **MANDATORY**. Every function signature must be typed.
    *   `def my_func(a: int) -> str:`
*   **Docstrings**: **MANDATORY**. Google Style docstrings for modules, classes, and public functions.
*   **File Size**: Max **300 lines**.
    *   If a file exceeds 300 lines -> Refactor/Split immediately.
*   **Function Size**: Max **30 lines**.
    *   Exceptions: `__init__`, heavy configuration dicts.
*   **Linter**: Code must pass `ruff check src/` with ZERO warnings.

## 2. Testing Standards (Strict)

*   **Coverage**: Business logic (`services/`) requires **90%+** coverage. Overall project **80%+**.
*   **Framework**: `pytest` only.
*   **Placement**: Tests strictly mirror the `src` structure.
    *   `src/services/user_service.py` -> `tests/services/test_user_service.py`
*   **Protocol**:
    *   Write tests *during* development (TDD preferred).
    *   **NEVER** delete a test to make the build pass. Fix the code.

## 3. Architecture

*   **Layered Architecture**:
    *   `src/api/` -> Entry points (CLI, HTTP). No business logic.
    *   `src/services/` -> Business logic. Pure Python. No SQL.
    *   `src/repositories/` -> Data access. SQL/Files. No business logic.
    *   `src/models/` -> Data classes (Pydantic).
*   **Data Flow**: `API -> Service -> Repository -> DB`.
*   **Dependencies**: Dependencies point **DOWN**. A Repository never imports a Service.

## 4. Documentation
*   **Artifacts**: Use high-quality markdown artifacts for plans and reports.
*   **Context**: Keep `.context/STATUS.md` updated as the "Single Source of Truth".

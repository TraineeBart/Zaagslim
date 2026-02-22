---
trigger: always_on
description: Skills reference table — maps skills to when they apply
---

# Development Rules

## Skills Reference

Apply these skills to all Python development work:

| Skill | When |
|---|---|
| Python Coding Standard | All Python code |
| Context Management | Every session start/end |
| Testing Standard | Writing and running tests |
| Git & Version Control | All commits and branching |
| API Design | REST endpoints, schemas, routes |

## Verification First

NEVER present work as "done" without running verification:
1. Run tests: `pytest --cov=src`
2. Run linter: `ruff check src/`
3. Confirm all pass BEFORE reporting to the user
4. If anything fails, fix it first — do not ask the user to fix lint/test issues you created

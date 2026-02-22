---
trigger: always_on
description: Safety guardrails — when to stop and check before proceeding
---

# Safety Guardrails

## Always STOP and Ask Before

- Changing project architecture or directory structure
- Adding new dependencies (packages, services, databases)
- Modifying or deleting database schemas
- Deleting or renaming existing files
- Changing public API contracts
- Making any change that affects more than 3 existing files
- Fixing something that wasn't asked for (note it, don't fix it)

## Scope Creep Prevention

- If you notice something that "should also be fixed" → note it in `.context/STATUS.md` under "Known Issues", do NOT fix it silently
- If a task reveals unexpected complexity → stop, update the plan, get approval
- Never combine unrelated changes in one session

## Context Recovery

- If `.context/` is missing or outdated → scan project, draft context files, confirm with user before proceeding
- NEVER start work without confirmed context

## Forbidden Actions

NEVER do any of these under any circumstances:
- Delete or overwrite existing tests without explicit approval
- Push to `main` branch directly
- Run destructive database operations (DROP, TRUNCATE) without confirmation
- Install system-level packages or modify system configuration
- Access or modify production data or credentials
- Remove safety checks, validation, or error handling to "simplify" code
- Commit secrets, tokens, or passwords to version control

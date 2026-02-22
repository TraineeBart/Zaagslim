---
description: Periodic project health check to prevent complexity drift and technical debt
---

# /health-check — Project Health Check

Run this workflow every **5 sessions** (or when starting a session after 2+ weeks gap).
At the start of each session, check `.context/STATUS.md` for the `Last health check` date.
If it has been 5+ sessions or 2+ weeks, run this workflow **before** starting any new work.

---

## Phase 1: Automated Diagnostics

Run all checks and collect results before analysis.

### 1.1 Test Suite Health
// turbo
```bash
cd /Users/bb2-1/Documents/Zaagslim && .venv/bin/python -m pytest tests/ --cov=src --cov-report=term-missing -q 2>&1 | tail -40
```

**Thresholds:**
- 🟢 0 failures, coverage ≥ 80%
- 🟡 0 failures, coverage 60-79%
- 🔴 Any failures OR coverage < 60%

### 1.1b Service Coverage Breakdown
// turbo
```bash
cd /Users/bb2-1/Documents/Zaagslim && .venv/bin/python -m pytest tests/ --cov=src/services --cov-report=term-missing -q 2>&1 | grep -E "^src/services/" | sort -t% -k4 -n | head -15
```

**Thresholds:**
- 🟢 All business services ≥ 90%
- 🟡 Business services 75-89%
- 🔴 Any business service < 75% OR overall services < 70%

### 1.2 Linter
// turbo
```bash
cd /Users/bb2-1/Documents/Zaagslim && .venv/bin/ruff check src/ tests/ --statistics 2>&1
```

**Threshold:** 🟢 = 0 errors. Any error = 🔴

### 1.3 File Size Audit
// turbo
```bash
cd /Users/bb2-1/Documents/Zaagslim && find src/ -name "*.py" -exec wc -l {} + | sort -rn | head -15
```

**Threshold:** Every `.py` file must be < 300 lines. Flag violations.

### 1.4 Function Length Audit
// turbo
```bash
cd /Users/bb2-1/Documents/Zaagslim && .venv/bin/python << 'PYEOF'
import ast, pathlib

violations = []
for f in pathlib.Path("src").rglob("*.py"):
    try:
        tree = ast.parse(f.read_text())
    except SyntaxError:
        continue
    for node in ast.walk(tree):
        if isinstance(node, (ast.FunctionDef, ast.AsyncFunctionDef)):
            length = node.end_lineno - node.lineno + 1
            if length > 30:
                violations.append((str(f), node.name, length))

if violations:
    print(f"⚠️  {len(violations)} functions exceed 30 lines:")
    for path, name, length in sorted(violations, key=lambda x: -x[2]):
        print(f"  {path}:{name} — {length} lines")
else:
    print("✅ All functions ≤ 30 lines")
PYEOF
```

### 1.5 Circular Import Check
// turbo
```bash
cd /Users/bb2-1/Documents/Zaagslim && .venv/bin/python -c "
import importlib, pkgutil, sys
errors = []
for importer, modname, ispkg in pkgutil.walk_packages(['src'], prefix='src.'):
    try:
        importlib.import_module(modname)
    except ImportError as e:
        errors.append(f'{modname}: {e}')
if errors:
    print('🔴 Import errors:')
    for e in errors: print(f'  {e}')
else:
    print('✅ No circular imports detected')
"
```

### 1.6 Dead Code Detection
// turbo
```bash
cd /Users/bb2-1/Documents/Zaagslim && .venv/bin/python -m pytest tests/ -q --co 2>&1 | tail -3 && echo "---" && grep -r "def " src/ --include="*.py" -l | wc -l | xargs -I{} echo "{} source files with functions"
```

### 1.7 Dependency Health
// turbo
```bash
cd /Users/bb2-1/Documents/Zaagslim && .venv/bin/pip list --outdated 2>/dev/null | head -15
```

---

## Phase 2: Architecture Review

Manually assess the following. For each item, record 🟢/🟡/🔴.

### 2.1 Dependency Direction
Verify that dependencies flow **downward only**:
```
CLI → Services → Repositories → Models
```
Check: do any lower layers import from higher layers?

### 2.2 Single Responsibility
For each module in `src/services/`, answer: "Can I describe what this module does in one sentence?"
If not → flag for splitting.

### 2.3 API Surface Area
Count public functions per module. If any module exposes > 10 public functions → flag for review.

### 2.4 Configuration Sprawl
Check: are there config values hardcoded in multiple places?
All configuration should flow through config classes or `settings`.

---

## Phase 3: Context & Documentation Audit

### 3.1 STATUS.md Accuracy
- Does "In Progress" reflect reality?
- Is the backlog still correctly prioritized?
- Are "Known Issues" still accurate or resolved?

### 3.2 DECISIONS.md Completeness
- Were any architectural decisions made since last check that aren't logged?

### 3.3 VISION.md Alignment
- Is the current work still aligned with the vision?
- Should priorities shift based on what we've learned?

### 3.4 Test Coverage Gaps
Run coverage report and identify untested critical paths:
- Services with < 80% coverage
- Any service with 0% coverage = 🔴

### 3.5 Skill & Workflow Audit
Review recent sessions and answer these questions:

1. **Repeated manual actions**: Are there actions performed 3+ times across sessions that should be a workflow (`.agent/workflows/`) or skill (`.agent/skills/`)?
2. **Anti-patterns**: Were any mistakes repeated? If so, add to `DECISIONS.md` → Anti-Patterns table.
3. **Stale workflows**: Do existing workflows still match reality?
4. **Missing skills**: Are there domains we've built deep knowledge in that aren't captured as a skill?

**Action**: Create/update workflows or skills as needed. Log any new anti-patterns.

---

## Phase 4: Scorecard

Compile results into this scorecard:

```markdown
## 🏥 Health Check — [DATE]

| Category              | Score | Notes                      |
|----------------------|-------|----------------------------|
| Tests passing        | 🟢/🟡/🔴 |                          |
| Test coverage        | ___%  |                            |
| Linter               | 🟢/🔴 |                            |
| File sizes           | 🟢/🟡/🔴 | N files over limit       |
| Function lengths     | 🟢/🟡/🔴 | N functions over limit   |
| Circular imports     | 🟢/🔴 |                            |
| Dependency direction | 🟢/🟡/🔴 |                          |
| Single responsibility| 🟢/🟡/🔴 |                          |
| Context docs current | 🟢/🟡/🔴 |                          |
| Vision alignment     | 🟢/🟡/🔴 |                          |

**Overall: [HEALTHY / NEEDS ATTENTION / AT RISK]**
```

**Decision rules:**
- All 🟢 → **HEALTHY** — proceed with new features
- Any 🟡 → **NEEDS ATTENTION** — fix before or alongside new work
- Any 🔴 → **AT RISK** — fix before ANY new features

---

## Phase 5: Action Plan

1. List all 🔴 items → create fix tasks, estimate effort
2. List all 🟡 items → add to next session backlog
3. Update `.context/STATUS.md` with:
   - `Last health check: [DATE]`
   - Any new Known Issues discovered
   - Backlog updates
4. Present scorecard to user for review
5. **Only after 🔴 items are resolved**: proceed with regular work

---

## Trigger Reminder

Add this line to `.context/STATUS.md` under a new section:

```markdown
## Health Check
- Last check: [DATE]
- Sessions since: 0
- Next due: after 5 sessions or 2 weeks
```

Increment "Sessions since" at the start of every session.

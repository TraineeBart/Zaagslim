# Architectural Decision Records

## Format

| # | Date | Decision | Rationale | Status |
|---|------|----------|-----------|--------|
| 1 | 2026-02-22 | Project structure mirrors Sniper-Lab agent protocol | Proven workflow, consistent developer experience across projects | Active |

---

## ADR-001: Agent Protocol Structure

**Date**: 2026-02-22
**Status**: Active

**Context**: New project needs consistent development workflow.

**Decision**: Mirror the `.agent/` (rules, skills, workflows) and `.context/` structure from Sniper-Lab.

**Rationale**: The Sniper-Lab agent protocol has been battle-tested across 50+ sessions and provides a solid foundation for quality, documentation, and consistency.

**Consequences**: All working agreements, code standards, and session protocols are inherited. Project-specific customizations can be layered on top.

# Architectural Decision Records

## Format

| # | Date | Decision | Rationale | Status |
|---|------|----------|-----------|--------|
| 1 | 2026-02-22 | Project structure mirrors Sniper-Lab agent protocol | Proven workflow, consistent developer experience across projects | Active |
| 2 | 2026-02-22 | Rebrand page to Zaagslim (not OptiCut AI) | Domain is zaagslim.nl, OptiCut AI reserved for international expansion | Active |
| 3 | 2026-02-22 | Static Nginx hosting, no Docker | Single HTML file, Docker is overkill. Revisit when backend is built | Active |
| 4 | 2026-02-22 | AJAX form submit instead of redirect | Keeps user in modal, enables Meta Pixel Lead event tracking | Active |
| 5 | 2026-02-22 | Meta Ads (not Google Ads) for validation | Demand creation > demand capture for niche market with low search volume | Active |

---

## ADR-001: Agent Protocol Structure

**Date**: 2026-02-22
**Status**: Active

**Context**: New project needs consistent development workflow.

**Decision**: Mirror the `.agent/` (rules, skills, workflows) and `.context/` structure from Sniper-Lab.

**Rationale**: The Sniper-Lab agent protocol has been battle-tested across 50+ sessions and provides a solid foundation for quality, documentation, and consistency.

**Consequences**: All working agreements, code standards, and session protocols are inherited. Project-specific customizations can be layered on top.

---

## ADR-002: Rebrand to Zaagslim

**Date**: 2026-02-22
**Status**: Active

**Context**: Domain is `zaagslim.nl` but landing page showed "OptiCut AI" branding.

**Decision**: Use "Zaagslim" as primary brand for Dutch market. Reserve "OptiCut AI" for future international expansion.

**Rationale**: Brand mismatch between domain and page content undermines trust with target audience (practical tradespeople).

---

## ADR-003: Static Nginx, No Docker

**Date**: 2026-02-22
**Status**: Active

**Context**: Hosting a single HTML landing page on an existing VPS with Docker available.

**Decision**: Use a simple Nginx server block. No Docker container.

**Rationale**: Docker adds unnecessary complexity for 1 static file. Revisit when the actual SaaS backend is built.

---

## ADR-004: AJAX Form + Meta Pixel Tracking

**Date**: 2026-02-22
**Status**: Active

**Context**: Need to measure conversion from ad click → wachtlijst signup.

**Decision**: Convert Formspree form to AJAX submit with in-modal thank-you state. Fire `fbq('track', 'Lead')` on successful signup.

**Rationale**: Page redirect breaks the user experience and loses conversion attribution. AJAX keeps the modal open and reliably fires the pixel event.

---

## ADR-005: Meta Ads for Validation

**Date**: 2026-02-22
**Status**: Active

**Context**: Need to validate market demand with €50 budget.

**Decision**: Use Meta Ads (Facebook) with demand-creation approach, not Google Ads.

**Rationale**: Search volume for "zaaglijst software" is negligible in NL. Target audience (interieurbouwers 35-55) is active on Facebook. Meta Ads allows interest-based targeting (Festool, houtbewerking, etc).

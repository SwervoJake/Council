# Blueprint Memory Index
**Last updated:** 2026-03-04

## Current Context
- Council deployed. Blueprint workspace active.
- Routing structure audit completed 2026-03-04. One Class B debt item: architecture-review-template.md referenced but not created during Phase 2 deployment.
- ADR-001 logged: routing structure audit findings.

## Key Decisions & Patterns
- **Thin wrapper pattern** for `.claude/agents/` — activation stub decoupled from identity schema. Identity lives in `workspace-*/CLAUDE.md`. Reduces duplication, simplifies routing updates.
- **Phase-gated deployment** — MVC (Phase 1: 19 files) before richness (Phase 2: 67 files) proved correct. No overload failures.
- **Ghost reference corrected** — `architecture-review-template.md` listed in CLAUDE.md and MEMORY.md but not created. Removed references. Template can be created when first complex review session warrants it.

## Files in This Memory
- `architecture-decisions/ADR-001-routing-structure-audit.md` — Full routing audit, 2026-03-04
- `tech-stack-context.md` — Current stack, versions, constraints, known limitations
- `tech-debt-register.md` — Active debt items with Class A/B/C, payback plan, owner
- `estimation-accuracy.md` — PERT estimate vs. actual outcome tracking

## Calibration Notes
*One session recorded. Blueprint's known bias pattern: accurate on scope, tends to underestimate integration complexity by ~20%. Monitor and confirm across first 10 sessions.*

## Templates Available
- `templates/adr-template.md` — Architecture Decision Record
- `templates/cost-estimate-template.md` — Cost breakdown structure
- `templates/tradeoff-matrix-template.md` — Multi-criteria tradeoff analysis

# Technical Patterns
*Transferable technical strategy patterns with confidence scores. Maintained by Blueprint + Atlas.*

**Scoring:** Starts 0.5. +0.05 per successful application. −0.10 per failure. Above 0.80 → COUNCIL_STATE.md doctrine. Below 0.30 → archived.

---

## Pattern: Three-Option Architecture Rule
- **Confidence:** 0.5
- **Applications:** 0
- **Last updated:** 2026-03-04
- **Pattern:** Every architectural recommendation provides three options (minimal/balanced/optimal). Prevents false binary choices and anchors decisions on a range, not a single proposal.
- **Conditions:** Any technical architecture or build decision.
- **Counter-evidence:** Emergency hotfixes where speed is paramount — single recommendation acceptable.
- **Source:** Factory Council architecture specification

---

## Pattern: PERT Estimation with Range
- **Confidence:** 0.5
- **Applications:** 0
- **Last updated:** 2026-03-04
- **Pattern:** Use PERT formula (O + 4M + P) / 6 for all timeline estimates. Always present the range (O–P), not just the point estimate. Prevents false precision and surfaces uncertainty explicitly.
- **Conditions:** Any engineering timeline estimate.
- **Counter-evidence:** Trivial tasks (<2 hours) where range is meaningless.
- **Source:** Factory Council architecture specification

---

## Pattern: Document Debt Class at Acceptance
- **Confidence:** 0.5
- **Applications:** 0
- **Last updated:** 2026-03-04
- **Pattern:** Every accepted technical shortcut is classified at acceptance (Class A/B/C) with a payback plan. Undocumented debt defaults to Class C (toxic). The act of classification reduces regret debt accumulation.
- **Conditions:** Any decision that knowingly accepts technical shortcuts.
- **Counter-evidence:** Fully greenfield work with no shortcuts — no debt to classify.
- **Source:** Factory Council architecture specification

---

## Pattern: Phase-Gated Deployment — MVC First, Richness Second
- **Confidence:** 0.5
- **Applications:** 1
- **Last updated:** 2026-03-04
- **Pattern:** Complex system deployments split into MVC (Minimum Viable Configuration) — essential function only — followed by Phase 2 (templates, enrichment, calibration infrastructure). Prevents cognitive overload during deployment execution and reduces error accumulation from scope creep during single session.
- **Conditions:** Multi-phase system deployments with 50+ files or more than 4 cross-connected subsystems. Inappropriate for <10 file, single-domain deployments.
- **Counter-evidence:** Emergency deployments where all-or-nothing is operationally required; single-phase rollouts that proved successful despite scale.
- **Source:** Factory Council memory system deployment (2026-03-04) — 86 files across two phases. Phase 1 (MVC) established routing, identity, and basic memory. Phase 2 added templates, strategy seeding, calibration tracking. Sage flagged high cognitive load for full deployment in one session; phasing mitigated the risk.
- **Outcome tracked:** Will compare against outcomes of first live strategic sessions to assess whether cognitive load reduction translated to fewer deployment errors.

---

*[Add patterns here as sessions accumulate and strategy learnings are extracted]*

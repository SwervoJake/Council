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

*[Add patterns here as sessions accumulate and strategy learnings are extracted]*

# Cost Estimate Template

---

## Cost Estimate: [Feature/Project]
**Date:** YYYY-MM-DD
**Requestor:** [which agent or operator requested this]
**Decision this informs:** [what decision depends on this estimate]

---

## PERT Timeline Estimate

| Component | Optimistic | Most Likely | Pessimistic | PERT Calc |
|-----------|-----------|-------------|-------------|-----------|
| [Component 1] | | | | |
| [Component 2] | | | | |
| [Integration] | | | | |
| [Testing/QA] | | | | |
| **Total** | | | | **[sum]** |

**PERT Formula:** (O + 4M + P) / 6
**Standard Deviation:** (P - O) / 6
**90% confidence range:** PERT ± 1.65 × StdDev

---

## Cost Breakdown

### Engineering (internal)
| Role | Hours | Rate | Total |
|------|-------|------|-------|
| [Engineer] | | | |
| **Subtotal** | | | |

### External / Tools / Infrastructure
| Item | One-time | Monthly | Annual |
|------|---------|---------|--------|
| [Item] | | | |
| **Subtotal** | | | |

### Total Cost
- **One-time build:** $[amount]
- **Ongoing monthly:** $[amount]
- **12-month total:** $[amount]

---

## Assumptions
| Assumption | Value | Impact if wrong |
|-----------|-------|----------------|
| | | |

---

## Sensitivity Analysis
*Which assumption, if wrong, changes the estimate most?*

**Critical assumption:** [name]
**If 2× off:** New estimate becomes $[amount] or [weeks]
**Mitigation:** [how to reduce this uncertainty]

---

## Three Options Summary
| Option | Build time | Cost | Tech debt | Recommendation |
|--------|-----------|------|-----------|---------------|
| Minimal | | | Class C | — |
| Balanced | | | Class B | ✓ Recommended |
| Optimal | | | None | — |

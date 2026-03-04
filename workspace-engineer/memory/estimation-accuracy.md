# Blueprint — Estimation Accuracy
*PERT estimate vs. actual outcome tracking. The primary calibration mechanism for Blueprint.*

---

## Tracking Format
```
## [Project/Task] — YYYY-MM-DD
- PERT estimate: [X weeks] (O: [optimistic], M: [most likely], P: [pessimistic])
- Actual: [Y weeks]
- Delta: [+/- Z weeks] ([+/-]%)
- Root cause of variance:
  - Scope changes: [Yes/No — description]
  - Integration complexity: [Yes/No — description]
  - External dependencies: [Yes/No — description]
  - Technical unknowns: [Yes/No — description]
- Learning for future estimates:
```

---

## Accuracy History

| Date | Task | PERT Est. | Actual | Delta | Root Cause |
|------|------|-----------|--------|-------|------------|
| *Populated after first sessions* | | | | | |

---

## Bias Analysis
*Updated monthly by Atlas during calibration:*

- **Overall accuracy:** *(calculated from history)*
- **Known biases:**
  - Integration complexity: Suspected 20% underestimate — confirm or refute from data
  - External dependencies: [Track here]
- **Calibration adjustment:** *(Atlas notes how Blueprint estimates are adjusted in synthesis)*

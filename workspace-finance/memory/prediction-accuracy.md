# Sterling — Prediction Accuracy
*Sterling's forecast vs. actual tracking. The primary calibration mechanism for financial projections.*

---

## Tracking Format
```
## [Prediction] — Made YYYY-MM-DD
- Prediction: [specific claim with number and timeframe]
- Outcome: [actual result — measured YYYY-MM-DD]
- Delta: [+/-% variance]
- Root cause of variance:
  - Market conditions: [description]
  - Assumption failure: [which assumption was wrong]
  - Execution: [execution factors that changed the outcome]
- Calibration update: [how to adjust future similar projections]
```

---

## Prediction Log

| Date Made | Prediction | Actual | Delta | Root Cause |
|-----------|-----------|--------|-------|------------|
| *(Populated after first financial sessions)* | | | | |

---

## Bias Analysis
*Updated monthly by Atlas during calibration:*

- **Revenue projection bias:** *(known: tendency toward 10–15% optimism — confirm or refute)*
- **CAC projection bias:** *(track here)*
- **Timeline bias:** *(track here)*
- **Calibration adjustment applied:** *(how Atlas weights Sterling inputs in synthesis)*

# Orbit — Channel Performance
*Channel CAC/LTV history, trends, and saturation signals. The acquisition engine's health record.*

---

## Channel Snapshot Format
```
## [Channel] — Updated YYYY-MM-DD
- CAC: $[amount]
- LTV: $[amount] (from cohort: [cohort date])
- LTV:CAC: [ratio]
- Payback period: [months]
- Monthly spend: $[amount]
- Monthly customers acquired: [count]
- Conversion rate: [%] at [stage]
- Scalability: [can spend more / approaching saturation / saturated]
- Trend: ↑ / → / ↓
```

---

## Active Channel Performance

*(Populate before first GTM session with your current channel mix)*

---

## Channel History

| Channel | Date | CAC | LTV:CAC | Payback | Status |
|---------|------|-----|---------|---------|--------|
| *(Populated as data accumulates)* | | | | | |

---

## Saturation Signals
*When to stop scaling a channel:*
- CAC increases >20% quarter-over-quarter
- Conversion rate drops >30% at any funnel stage
- CPC / CPM increases >40% without compensating LTV improvement
- Orbit flags: `[CROSS-CHECK: STERLING]` when saturation is detected

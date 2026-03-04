# Council Usage Tracker

Tracks token efficiency per session. Updated at session close.
Governs the monthly calibration check on Router accuracy.

**Protocol reference:** `.claude/rules/usage-reduction-protocol.md`
**Router agent:** `.claude/agents/router.md`

---

## Efficiency Score Formula

```
Efficiency score = (Agents actually needed / Agents invoked) × 100

"Agents actually needed" = agents whose output materially changed the Atlas synthesis.
An agent invoked but whose output did not influence the synthesis = not needed.
```

| Score | Rating | Action |
|-------|--------|--------|
| 90–100% | Optimal | No adjustment |
| 70–89% | Good | Note unnecessary agent(s) |
| 50–69% | Moderate waste | Review Router tier assignment |
| < 50% | High waste | Flag Router for calibration |

---

## Session Log

| Date | Topic | Tier | Agents invoked | Agents needed | Efficiency | Cache hit? | Notes |
|------|-------|------|----------------|---------------|------------|-----------|-------|
| — | — | — | — | — | — | — | No sessions logged yet |

---

## Cache Hit Rate (monthly)

Track how often Router returns a cache hit vs. a miss.
High cache hit rate = system is compounding intelligence correctly.
Low cache hit rate after 3+ months = strategies/ not being populated.

| Month | Sessions | Cache hits | Hit rate | Avg efficiency score |
|-------|----------|-----------|---------|----------------------|
| — | — | — | — | — |

---

## Router Calibration Log

When Router assigns the wrong tier (discovered at session close via efficiency score < 70%):

| Date | Question type | Router tier | Actual tier needed | Error direction | Pattern |
|------|--------------|-------------|-------------------|-----------------|---------|
| — | — | — | — | — | — |

**Error direction:**
- Over-tiered: Router said T3, T1 was sufficient (wastes tokens)
- Under-tiered: Router said T1, T3 was needed (risks quality)

Under-tiering is worse than over-tiering. If Router consistently under-tiers
a question type, adjust the classification criteria in `router.md`.

---

## Monthly Summary (auto-populate at calibration session)

### Target benchmarks (by month 3 of operation)
- Cache hit rate: ≥ 40% (most strategic questions have precedent by month 3)
- Average efficiency score: ≥ 75%
- Router mis-tier rate: ≤ 15%
- T4 debates per month: ≤ 2 (debate is the highest-cost mode)

### If benchmarks are missed:
- Hit rate < 40%: Strategies/ not being populated after sessions. Check session closure protocol.
- Efficiency < 75%: Atlas is adding agents beyond Router's minimum set. Review Atlas behavior.
- Mis-tier > 15%: Router classification criteria need tuning. Review `router.md` tier table.
- T4 > 2/month: Operator is bringing too many irreversible questions to council. Consider offline journaling or deferred questions before live sessions.

---

## Cost Reference (Claude Pro context)

Jacob's plan: Claude Pro ($20/month)
Effective token budget per month: Approximately 10–15 full council sessions
OR: 60–90 targeted T1 sessions OR: any combination.

**Every unnecessary full council session costs the equivalent of 10–15 T1 sessions.**

---

*Last updated: 2026-03-04*
*Populated by: Atlas at session close*

# Agent Accuracy Calibration
*Atlas maintains this file. Updated monthly by comparing past predictions against actual outcomes.*

**Purpose:** Track each agent's prediction accuracy over time. Calibrate how Atlas weights agent outputs in synthesis. Compound the council's intelligence.

---

## Sterling — Financial Projections

| Date | Prediction | Actual | Delta | Notes |
|------|-----------|--------|-------|-------|
| *(First entry after a Sterling prediction is testable)* | | | | |

**Running accuracy:** *(calculated after 5+ entries)*
**Known bias:** Tendency toward 10–15% revenue optimism — apply downside adjustment until history confirms or refutes.
**Atlas weighting note:** *(updated monthly)*

---

## Blueprint — Timeline Estimates

| Date | Estimate (PERT) | Actual | Delta | Root Cause |
|------|----------------|--------|-------|------------|
| *(First entry after a Blueprint estimate is testable)* | | | | |

**Running accuracy:** *(calculated after 5+ entries)*
**Known bias:** Suspected 20% underestimate on integration complexity — confirm from data.
**Atlas weighting note:** *(updated monthly)*

---

## Orbit — Growth Projections

| Date | Projection | Actual | Delta | Notes |
|------|-----------|--------|-------|-------|
| *(First entry after an Orbit projection is testable)* | | | | |

**Running accuracy:** *(calculated after 5+ entries)*
**Known pattern:** Churn estimates tend to be more reliable than Sterling's retention projections.
**Atlas weighting note:** *(updated monthly)*

---

## Ward — Risk Assessments

| Date | Risk Rated | Materialized? | Assessment | Notes |
|------|-----------|--------------|------------|-------|
| *(First entry after a Ward risk assessment can be evaluated)* | | | | |

**RED accuracy:** *(% of RED ratings that materialized as blocking issues)*
**AMBER accuracy:** *(% of AMBER ratings where mitigations were sufficient)*
**Known pattern:** RED ratings historically reliable — track false alarm rate.
**Atlas weighting note:** *(updated monthly)*

---

## Muse — Idea Outcomes

| Date | Selected Idea | Built? | Outcome | Score vs. Expectation |
|------|-------------|--------|---------|----------------------|
| *(First entry after a Muse recommendation gets built and measured)* | | | | |

**Wildcard hit rate:** *(% of wildcards that became the chosen direction)*
**Curation accuracy:** *(% of top-scored ideas that outperformed lower-scored ones)*
**Atlas weighting note:** *(updated monthly)*

---

## Sage — Flag Accuracy

| Date | Flag | Context | Outcome if Followed | Outcome if Ignored |
|------|------|---------|--------------------|--------------------|
| *(First entry after a Sage flag recommendation can be evaluated)* | | | | |

**Flag calibration:** *(are flags triggering at appropriate thresholds?)*
**Known pattern:** Calibrates to specific operator over 10+ sessions.
**Atlas weighting note:** *(updated monthly)*

---

## Calibration Insights
*Updated monthly by Atlas. The actionable intelligence extracted from accuracy tracking.*

*(No insights yet. First entries after 3+ months of calibration data.)*

---

## Calibration Protocol
**Frequency:** Monthly
**Process:**
1. Review each agent's predictions made in the past month
2. Compare against measurable outcomes where available
3. Update running accuracy and delta tables above
4. Note any systematic bias patterns emerging
5. Update Atlas weighting notes for next month's synthesis
6. Review strategy patterns in `shared-knowledge/strategies/` — update confidence scores
7. Archive strategies below 0.30; promote above 0.80 to COUNCIL_STATE.md

# Sequential Pipeline Handoff Template

Use when one agent's output is the direct input for the next. Write a handoff file after each stage.

---

## Handoff: [TOPIC] — Stage [N] to Stage [N+1]
**Date:** YYYY-MM-DD
**From:** [Agent A]
**To:** [Agent B]
**Pipeline step:** [N of total]

---

## What I Did
*[Brief description of the analysis or output produced in this stage.]*

---

## My Output
*[The actual output — financial model, architecture recommendation, risk assessment, etc.]*

---

## Key Assumptions I Made
*[What Agent B needs to know about the assumptions built into my output.]*

| Assumption | Value used | Basis | Confidence |
|-----------|-----------|-------|-----------|
| | | | |

---

## What You Need to Do With This
*[Specific question or task for the next agent. Be precise.]*

**Your task:** [clear directive]
**Specific questions to answer:**
1.
2.

---

## What I Could Not Assess (Your Domain)
*[What's out of scope for my analysis that Agent B needs to address.]*

-

---

## Cross-Check Flags Raised
*[Any flags for other agents beyond the next in the pipeline.]*

-

---

## Quality Check Before Passing
- [ ] My output is self-contained — Agent B has everything needed
- [ ] Assumptions are explicit, not buried
- [ ] I've named what I don't know
- [ ] Confidence level stated on every recommendation

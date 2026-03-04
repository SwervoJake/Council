# Output Standards

All Factory Council agent outputs must conform to these standards. No exceptions — the standards are what make outputs comparable, synthesizable, and trustworthy over time.

---

## Universal Requirements

Every agent output must include:

### 1. Confidence Level
**HIGH / MEDIUM / LOW** — on every recommendation. Never omit.

```
Confidence: HIGH — Multiple agents agree, strong evidence, low uncertainty
Confidence: MEDIUM — Mixed signals, reasonable assumptions, some uncertainty
Confidence: LOW — Significant disagreement, weak evidence, high uncertainty
```

Do not use percentages or scores at this tier. The qualitative rating is intentional — it forces a judgment call rather than false precision.

### 2. Risk Rating
**RED / AMBER / GREEN** — on every risk assessment. Never omit.

```
RED    — Stop. Material exposure. Resolve before proceeding.
AMBER  — Proceed with specific, named mitigations. Document them.
GREEN  — No blocking issues. Note ambient risks for awareness only.
```

### 3. Self-Assessment
Every agent session ends with its agent-specific self-assessment template (see each agent's CLAUDE.md). Self-assessment is not optional — it is the calibration mechanism.

---

## Agent-Specific Requirements

### Atlas (synthesis outputs additionally require)
- Execution mode used and routing rationale
- Reversibility classification: easily reversible / partially reversible / irreversible
- Kill criteria with numeric, time-bound thresholds
- Acknowledgment of dissenting positions (named, not papered over)
- Knowledge base update entry

### Blueprint (every output)
- Three options: Minimal / Balanced / Optimal
- PERT timeline with range: (O + 4M + P) / 6
- Complexity score: 1–10
- Technical debt classification: Class A / B / C

### Muse (every output)
- Creative mode declared: Diverge / Curate / Plan / Advise
- Wildcard labeled: `[WILDCARD]`
- Assumption audit included

### Sterling (every output)
- Three-scenario model: Best / Base / Worst with probabilities
- Back-of-envelope calculation for any financial claim
- Kill criteria with numeric thresholds

### Ward (every output)
- Risk rating: RED / AMBER / GREEN (never omitted)
- Governing legal principle cited
- "Needs a lawyer" vs. "needs awareness" distinction explicit

### Orbit (every output)
- JTBD persona
- Positioning statement
- Channel unit economics per channel recommended
- Measurement framework (leading + lagging indicators)

### Sage (every output)
- Pillar assessment (which pillar(s) flagged)
- Sage flag if warranted
- Minimum effective dose recommendation

---

## Financial Claims Standard

Any output containing financial figures must include a back-of-envelope calculation showing how the number was derived. No unsubstantiated figures.

```
Example:
Estimated CAC: $320
Derivation: $16K/month channel spend ÷ 50 new customers/month = $320 CAC
Assumption: 50 customers/month based on 2% conversion of 2,500 monthly visitors
```

---

## Confidence × Reversibility Decision Gate

| Confidence | Reversibility | Required action |
|------------|--------------|-----------------|
| HIGH | Easily reversible | Proceed |
| HIGH | Irreversible | Proceed with kill criteria |
| MEDIUM | Easily reversible | Proceed |
| MEDIUM | Irreversible | Flag `[SAGE: DEFER]` — sleep on it |
| LOW | Easily reversible | Proceed with monitoring |
| LOW | Irreversible | Do not proceed without additional research |

---

## Strategy Confidence Scores (Tier 3 Memory)

When recording patterns to `shared-knowledge/strategies/`:
- Start at **0.5**
- **+0.05** per successful application
- **−0.10** per failure (asymmetric — prevents overconfidence)
- Above **0.80** → promoted to COUNCIL_STATE.md as established doctrine
- Below **0.30** → archived with failure postmortem

Always record as decimal (0.0–1.0), never as percentage.

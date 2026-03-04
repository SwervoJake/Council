# [Topic]
**Date:** YYYY-MM-DD
**Execution mode:** [parallel / sequential / debate / targeted / review]
**Agents activated:** [list]

---

## Invocation Audit

| Agent | Method | Timestamp | Reason (if not live) | Confidence modifier |
|-------|--------|-----------|----------------------|---------------------|
| Atlas | [live / synthesized / deferred] | [HH:MM UTC or —] | [— or reason] | [baseline or -1 level or N/A] |
| Blueprint | [live / synthesized / deferred] | [HH:MM UTC or —] | [— or reason] | [baseline or -1 level or N/A] |
| Muse | [live / synthesized / deferred] | [HH:MM UTC or —] | [— or reason] | [baseline or -1 level or N/A] |
| Sterling | [live / synthesized / deferred] | [HH:MM UTC or —] | [— or reason] | [baseline or -1 level or N/A] |
| Ward | [live / synthesized / deferred] | [HH:MM UTC or —] | [— or reason] | [baseline or -1 level or N/A] |
| Orbit | [live / synthesized / deferred] | [HH:MM UTC or —] | [— or reason] | [baseline or -1 level or N/A] |
| Sage | [live / synthesized / deferred] | [HH:MM UTC or —] | [— or reason] | [baseline or -1 level or N/A] |

**Synthesis confidence adjustment:**
- Live agents: [list]
- Synthesized agents: [list + reason or "None"]
- Deferred agents: [list + reason or "None"]
- Ceiling applied: [HIGH / MEDIUM / LOW — per invocation-audit-protocol.md scoring table]
- Net effect: [plain-language summary of what this means for this session's decision quality]

Full schema and scoring rules: `.claude/rules/invocation-audit-protocol.md`

---

## Agent Outputs Summary

### Atlas
- Task classification:
- Execution mode selected:
- Routing rationale:

### [Agent Name]
- Key recommendation:
- Confidence: [HIGH / MEDIUM / LOW]
- Risk rating: [RED / AMBER / GREEN]
- Cross-check flags raised:

### [Agent Name]
- Key recommendation:
- Confidence: [HIGH / MEDIUM / LOW]
- Risk rating: [RED / AMBER / GREEN]
- Cross-check flags raised:

---

## Atlas Synthesis
- **Decision:**
- **Confidence:** [HIGH / MEDIUM / LOW]
- **Reversibility:** [easily / partially / irreversible]
- **What drove the decision:**
- **Acknowledged dissent:**
- **Kill criteria:**
- **Action items:**
  - [ ]
  - [ ]

---

## Knowledge Base Update
- Strategy extracted: [title — if any]
- Domain: [financial / technical / market / legal / creative / health]
- Starting confidence: 0.5
- Store in: `shared-knowledge/strategies/[domain]-patterns.md`
- COUNCIL_STATE.md update needed: [Yes / No — if yes, what]
- Calibration update needed: [Yes / No — if yes, which agent]

---

## Sage Assessment
- Session load level: [LOW / MODERATE / HIGH / CRITICAL]
- Flags triggered: [None / REST / DEFER / LOAD / CHECK-IN]
- Notes:

---

## Usage Efficiency

- **Router invoked:** [Yes / No — if No, explain why]
- **Cache verdict:** [HIT (source: ___) / MISS]
- **Tier assigned by Router:** [T1 / T2 / T3 / T4]
- **Agents in Router's minimum set:** [list]
- **Agents actually invoked:** [list]
- **Agents added beyond Router's set:** [list + reason, or None]
- **Agents whose output materially changed synthesis:** [list]
- **Efficiency score:** [needed / invoked × 100 = ___%]
- **Efficiency rating:** [Optimal / Good / Moderate waste / High waste]
- **Record in:** `shared-knowledge/usage-tracker.md`

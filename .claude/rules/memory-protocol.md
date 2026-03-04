# Memory Protocol

This file governs how the three-tier memory system operates across all council sessions.

---

## Three Tiers Summary

| Tier | Storage | What it holds | Who manages it |
|------|---------|---------------|----------------|
| Tier 1 | Claude built-in | User context, persistent facts, preferences | Auto-loaded by Claude |
| Tier 2 | CLAUDE.md + logs | Agent identity (slow-changing) + session logs | Agent + operator |
| Tier 3 | strategies/ + calibration/ | Transferable patterns with confidence scores | Atlas + agents |

---

## Session Initiation Protocol

**At the start of every council session:**

1. **Atlas loads:** `shared-knowledge/COUNCIL_STATE.md` — current company context, active questions, established doctrine
2. **Each workspace agent auto-loads** its `workspace-[name]/CLAUDE.md` — identity, protocols, cross-check targets
3. **Agents optionally read** their `workspace-[name]/memory/MEMORY.md` — session context index
4. **Templates and memory sub-files** are loaded on-demand, not at startup

---

## Session Closure Protocol

**At the end of every council session:**

1. **Create session log** at `logs/YYYY-MM-DD-[topic].md` using the template below
2. **Complete the invocation audit section** — mandatory for every session log. Schema and scoring rules in `.claude/rules/invocation-audit-protocol.md`
3. **Update agent memory files** for any agent whose session produced new patterns or decisions
4. **Extract strategies** to `shared-knowledge/strategies/[domain].md` for any transferable pattern
5. **Update COUNCIL_STATE.md** if a decision reached HIGH confidence and is now established doctrine
6. **Update calibration** at `shared-knowledge/calibration/agent-accuracy.md` if a prediction was tested

---

## Session Log Format

```markdown
# [Topic]
**Date:** YYYY-MM-DD
**Execution mode:** [parallel / sequential / debate / targeted / review]
**Agents activated:** [list]

## Agent Outputs Summary

### [Agent Name]
- Key recommendation:
- Confidence: [HIGH / MEDIUM / LOW]
- Risk rating: [RED / AMBER / GREEN]
- Cross-check flags raised: [list or None]

## Atlas Synthesis
- Decision:
- Confidence: [HIGH / MEDIUM / LOW]
- Reversibility: [easily / partially / irreversible]
- What drove the decision:
- Acknowledged dissent:
- Kill criteria:
- Action items:

## Knowledge Base Update
- Strategy extracted: [title + confidence 0.5 to start]
- COUNCIL_STATE.md updated: [Yes / No — what changed]
- Calibration updated: [Yes / No]
```

Log files go in: `logs/YYYY-MM-DD-[topic].md`
Handoff files go in: `logs/handoffs/`
Debate records go in: `logs/debates/`

---

## Confidence Score Rules (Tier 3)

Confidence scores track how reliable each strategy pattern has proven to be.

```
Starting confidence: 0.5
Per successful application: +0.05
Per failure: -0.10 (asymmetric — prevents overconfidence)

Above 0.80 → promote to COUNCIL_STATE.md as established doctrine
Below 0.30 → archive to shared-knowledge/decisions/archived/ with failure postmortem
```

**Strategy format** (in `shared-knowledge/strategies/[domain].md`):
```markdown
## Strategy: [Title]
- Confidence: [0.0–1.0]
- Applications: [count]
- Last updated: YYYY-MM-DD
- Pattern: [generalizable description — when to use this]
- Conditions: [context where this applies]
- Counter-evidence: [when it fails or doesn't apply]
- Source session: [log file reference]
```

---

## Calibration Protocol (Monthly)

Run monthly using the Cowork scheduled task:

1. Open `shared-knowledge/calibration/agent-accuracy.md`
2. Review each agent's predictions against known outcomes
3. Update accuracy tracking table
4. Adjust Atlas's synthesis weighting notes based on observed agent biases
5. Archive strategy patterns below 0.30 confidence
6. Promote patterns above 0.80 to COUNCIL_STATE.md

---

## MEMORY.md Index Format

Each workspace's `MEMORY.md` is the auto-loaded index — the first file Claude reads in that agent's workspace. Keep it concise (under 80 lines):

```markdown
# [Agent] Memory Index
**Last updated:** YYYY-MM-DD

## Current Context
[What's active right now — 3-5 bullet points max]

## Key Decisions & Patterns
[Most important learnings from past sessions — brief, scannable]

## Files in This Memory
- [filename.md] — [one line description]
- [filename.md] — [one line description]

## Calibration Notes
[Known biases or accuracy patterns for this agent]
```

---

## @-Import Strategy

Use `@` imports sparingly — only files worth loading at session startup:

| File | When to @-import |
|------|-----------------|
| `atlas_framework.md` | In `workspace-ceo/CLAUDE.md` — full methodology on demand |
| `shared-knowledge/COUNCIL_STATE.md` | In `workspace-ceo/CLAUDE.md` — Atlas always loads fresh state |
| Other `*_framework.md` files | In their respective workspace CLAUDE.md |

**Do NOT** @-import templates, memory sub-files, or strategy files at startup — load on demand only.

---

## Privacy Note

Session logs may contain sensitive business context (financials, strategy, personnel). For public repositories, consider adding `logs/*.md` to `.gitignore`. The `.gitignore` in this repo notes this option — the operator decides.

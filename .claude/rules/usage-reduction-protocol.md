# Usage Reduction Protocol

This protocol governs how the Factory Council minimizes token consumption,
reduces unnecessary agent invocations, and preserves Claude Pro capacity for
high-value strategic work. It does not lower output quality — it eliminates
waste while maintaining rigor where stakes demand it.

**Target reduction:** 40–60% fewer tokens on cached or low-complexity questions.
**Quality preservation:** No reduction for T3/T4 sessions. Full standards apply.

---

## Core Principle

**Invoke the minimum number of agents needed to reach sufficient confidence
on this specific question at this specific stakes level.**

The default is NOT "full council." The default is "what's the smallest set
that produces a trustworthy answer?" Full council is reserved for T4.

---

## Step 0 — Route Through Router First (mandatory)

Before invoking Atlas or any domain agent, invoke the `router` agent.
The Router performs cache lookup and tier classification in a single Haiku call
(low-cost). It returns either:

- **CACHE HIT** → return the cached answer, no further invocation needed
- **CACHE MISS + Tier + Agent set** → proceed with the minimum viable set

**Never skip the Router.** Routing through Atlas directly without Router wastes
tokens on classification work that Haiku can do for ~200 tokens.

---

## Tier Summary

| Tier | Agents | Mode | Budget | When |
|------|--------|------|--------|------|
| T1 | 1–2 | Targeted | 2,000–4,000 | Single domain, low stakes, reversible |
| T2 | 2–3 | Parallel / Sequential | 4,000–8,000 | 2-3 domains, medium stakes |
| T3 | 4–5 | Parallel Council | 8,000–16,000 | Multi-domain, high stakes |
| T4 | 6–7 + Debate | Debate | 16,000–32,000 | Irreversible, critical stakes |

---

## Cache-First Lookup Rules

Cache lookup happens in Router (Step 0) and takes priority over all invocations.

### Confidence thresholds for cache use

| Source | Confidence threshold | Use without invocation? |
|--------|---------------------|------------------------|
| COUNCIL_STATE.md established doctrine | ≥ 0.80 | Yes — return directly |
| Strategy patterns | ≥ 0.70 | Yes — return with caveat |
| Strategy patterns | 0.50–0.69 | No — use as context, still invoke |
| Session logs (< 14 days old) | HIGH confidence | Yes — cite and return |
| Session logs (> 14 days old) | Any | No — may be outdated |
| Agent memory files | Any | No — use as context only |

### Cache hit caveat language

When returning a cache hit with confidence 0.70–0.79:
> "This answer is drawn from an existing strategy pattern (confidence: X.XX).
> It has not been re-validated by a live agent in this session. Proceed if the
> stakes are LOW to MEDIUM. Re-validate with a live agent if stakes are HIGH
> or CRITICAL before irreversible action."

---

## Compressed Output Mode (T1 only)

For T1 sessions (targeted, low stakes), agents use compressed output format.
Full output standards are suspended except for confidence and risk rating.

### T1 compressed format
```
**[Agent] — Compressed Output**
- Recommendation: [1-3 sentences]
- Confidence: [HIGH / MEDIUM / LOW]
- Risk: [RED / AMBER / GREEN]
- Key assumption: [the one assumption this depends on]
- Cache this? [Yes — if HIGH confidence and generalizable | No]
```

Self-assessment, back-of-envelope, three-option frameworks, wildcard, JTBD
persona, and other extended formats are **suspended** for T1 sessions.

T2, T3, T4: full output standards apply without exception.

---

## Session Batching Protocol

Running multiple small questions as separate sessions is the primary source of
wasted usage in this system. Batch before invoking.

### Batching rule
If the operator has 2 or more questions in the same session window:
1. Collect all questions before invoking Router
2. Router classifies them together
3. If they share domain, combine into a single multi-part T1 or T2 session
4. If they conflict in domain, run sequentially within one session (not as separate sessions)

**Estimated savings:** 30–50% reduction vs. running questions as separate sessions.
Each session has ~500–800 tokens of setup overhead (state loading, identity loading).
Batching eliminates that overhead on all but the first question.

---

## COUNCIL_STATE.md Pruning Protocol (Monthly)

COUNCIL_STATE.md grows with each session. Unbounded growth increases the token
cost of every Atlas load. Prune monthly using this protocol.

### Pruning rules

| Section | Keep? | When to archive |
|---------|-------|-----------------|
| Established doctrine (confidence ≥ 0.80) | Always | Never prune |
| Active strategic questions | Until resolved | Archive when decision reached |
| Operator context | Keep current only | Archive superseded facts |
| Session summaries | Last 3 only | Compress older to 1-line entries |

### Archive target
`shared-knowledge/decisions/archived/YYYY-MM-COUNCIL-STATE-archive.md`

### Pruning frequency
Monthly — align with confidence calibration session (already scheduled).
Run pruning before calibration to reduce context load during calibration.

**Target:** Keep COUNCIL_STATE.md under 150 lines at all times.
Current size: ~117 lines. Pruning needed when approaching 150 lines.

---

## Session Log Compression Protocol (Weekly)

Session logs older than 30 days are compressed. Compression extracts the
Atlas synthesis (decision + kill criteria + action items) and discards the
full agent output detail. The full log is moved to archive.

### Compression trigger
```
Age > 30 days AND decision status = closed (action items completed or abandoned)
```

### Compression target
```
logs/handoffs/YYYY-MM-DD-[topic]-compressed.md
```

### Compressed log format
```markdown
# [Topic] — Compressed
**Original date:** YYYY-MM-DD
**Execution mode:** [mode]
**Agents invoked:** [count] live, [count] synthesized

**Decision:** [Atlas synthesis decision — verbatim]
**Confidence:** [H/M/L]
**Kill criteria:** [verbatim]
**Outcome:** [what actually happened — filled in retrospectively]
**Strategy extracted:** [Yes — see strategies/[domain].md | No]
```

**Estimated savings:** Compressed logs are ~10 lines vs ~200 lines.
Reading 10 compressed logs vs 10 full logs saves ~1,900 lines of context.

---

## Agent Invocation Cost Reference

Use this when making tier decisions. Every invocation has a token cost.

| Agent | Typical token cost per live invocation |
|-------|---------------------------------------|
| Router (Haiku) | ~200–400 tokens (cheapest call possible) |
| Atlas (Sonnet) | ~1,500–3,000 tokens |
| Blueprint (Sonnet) | ~1,500–2,500 tokens |
| Sterling (Sonnet) | ~1,500–2,500 tokens |
| Muse (Sonnet) | ~1,500–2,500 tokens |
| Ward (Sonnet) | ~1,500–2,500 tokens |
| Orbit (Sonnet) | ~1,500–2,500 tokens |
| Sage (Sonnet) | ~1,000–2,000 tokens |

**Full 7-agent debate session:** ~25,000–50,000 tokens
**T1 targeted session (with Router):** ~2,200–4,400 tokens
**Savings of routing T1 correctly vs full council:** ~20,000–45,000 tokens

---

## Anti-Patterns (do not do these)

These patterns waste the most tokens and should be actively avoided:

| Anti-pattern | Why it wastes tokens | Fix |
|---|---|---|
| Invoking full council for a single-domain question | 6 agents invoked unnecessarily | Router → T1 |
| Running Atlas without Router first | Atlas re-does classification work | Always run Router first |
| Separate sessions for related questions | Repeated state-loading overhead | Batch questions |
| Loading all framework files at startup | ~1,500 lines loaded for 1-agent session | On-demand only |
| Re-deriving answers already in strategies/ | Pattern exists, agents re-derive from scratch | Cache-first lookup |
| Debate mode for reversible decisions | 3 rounds × 7 agents = max token burn | Reserve debate for T4 |
| Synthesizing 5+ agents due to context pressure | Confidence auto-degrades to LOW | Defer non-critical agents explicitly |

---

## Usage Efficiency Score (per session)

At session close, calculate an efficiency score and record it in the session log.
This score measures how well the minimum viable agent set was used.

```
Efficiency score = (Agents actually needed / Agents invoked) × 100

Where "agents actually needed" = agents whose output materially changed the Atlas synthesis.
If an agent was invoked but their output did not change the synthesis: not needed.
```

| Score | Rating | Action |
|-------|--------|--------|
| 90–100% | Optimal | No adjustment needed |
| 70–89% | Good | Note which agent(s) were unnecessary |
| 50–69% | Moderate waste | Review Router verdict for pattern |
| < 50% | High waste | Flag for calibration — Router may be mis-tiering |

Record in: `shared-knowledge/usage-tracker.md`

---

## Implementation Checklist (for Atlas)

When receiving any strategic question:

- [ ] Invoke Router first (Haiku call, ~300 tokens)
- [ ] If CACHE HIT with confidence ≥ threshold → return cached answer, done
- [ ] If CACHE MISS → use Router's tier and minimum agent set
- [ ] Do not add agents beyond Router's minimum set without documented reason
- [ ] For T1 sessions: use compressed output mode
- [ ] For T4 sessions: trigger `[SAGE: LOAD]` flag in synthesis
- [ ] At session close: calculate usage efficiency score
- [ ] Record score in `shared-knowledge/usage-tracker.md`

---

*Last updated: 2026-03-04*
*Governed by: `.claude/rules/usage-reduction-protocol.md`*
*Usage tracker: `shared-knowledge/usage-tracker.md`*

# Invocation Audit Protocol

This file defines the schema, scoring rules, and examples for recording how each agent was invoked in a council session. The invocation audit section is mandatory in every session log.

The problem this solves: session logs previously recorded *what* agents recommended but not *whether they were actually invoked*. A synthesized voice (Atlas internally modeling another agent) carries different reliability than a live invocation. Without this distinction, decision confidence is systematically overstated.

---

## Schema

Each agent entry in the invocation audit uses this structure:

```markdown
### [Agent Name]
- Invocation method: [live | synthesized | deferred]
- Timestamp: [HH:MM UTC — live only; omit if synthesized or deferred]
- Reason if synthesized: [context window constraint | blocking dependency | out of scope | time constraint | operator override]
- Reason if deferred: [out of scope | blocking dependency unresolved | not activated this session | scheduled for follow-up]
- Confidence modifier: [see scoring rules below]
```

**Field definitions:**

| Field | Description |
|-------|-------------|
| `live` | Agent was invoked via Agent tool. Output is first-person from that agent's identity schema and workspace. |
| `synthesized` | Atlas generated the agent's perspective internally. Voice is modeled, not live. Output quality depends on Atlas's internal model of that agent. |
| `deferred` | Agent was not consulted at all this session. No output recorded. |
| `Timestamp` | UTC time of live invocation. Omit for synthesized and deferred. |
| `Reason if synthesized` | Required. Must name one of the canonical reasons. "Unknown" is not acceptable. |
| `Reason if deferred` | Required. Must name one of the canonical reasons. |
| `Confidence modifier` | How this invocation method adjusts the weight of this agent's output in Atlas synthesis. |

---

## Confidence Modifier Rules

The invocation method affects how much weight Atlas should assign to an agent's output.

| Invocation method | Confidence modifier | Effect on output weight |
|-------------------|--------------------|-----------------------|
| `live` | +0 (baseline) | Full weight. Output is first-person from the agent's identity and workspace context. |
| `synthesized` | -1 level | Downgrade confidence one level: HIGH → MEDIUM, MEDIUM → LOW. Atlas is modeling the agent, not invoking it. |
| `deferred` | N/A | No output to weight. The missing voice is flagged as a gap, not a confidence level. |

**Atlas synthesis confidence rule:**

If 3 or more agents in a session are `synthesized` or `deferred`, the Atlas synthesis confidence ceiling is MEDIUM regardless of individual agent confidence levels. The reasoning: a synthesis of modeled voices is structurally less reliable than a synthesis of live voices.

```
Synthesis confidence ceiling:
  0 synthesized/deferred agents  → ceiling: HIGH (no cap)
  1-2 synthesized/deferred       → ceiling: HIGH (minor note in acknowledged dissent)
  3-4 synthesized/deferred       → ceiling: MEDIUM
  5-6 synthesized/deferred       → ceiling: LOW
  All agents synthesized/deferred → decision should not proceed; flag [SAGE: DEFER]
```

**Domain criticality modifier:**

Some agent voices carry higher stakes for specific decision types. If a domain-critical agent is synthesized or deferred, apply an additional confidence penalty:

| Decision domain | Domain-critical agents |
|-----------------|----------------------|
| Financial viability | Sterling (synthesized → MEDIUM cap regardless of others) |
| Legal/compliance | Ward (synthesized → flag [ESCALATE: EXTERNAL]) |
| Market/GTM strategy | Orbit (synthesized → MEDIUM cap on GTM recommendations) |
| Technical feasibility | Blueprint (synthesized → MEDIUM cap on architecture decisions) |

---

## Session Log Placement

The invocation audit block appears at the top of the session log, immediately after the metadata block and before Agent Outputs Summary.

```markdown
# [Topic]
**Date:** YYYY-MM-DD
**Execution mode:** [...]
**Agents activated:** [...]

## Invocation Audit

| Agent | Method | Timestamp | Reason (if not live) | Confidence modifier |
|-------|--------|-----------|----------------------|---------------------|
| Atlas | live | HH:MM UTC | — | baseline |
| Blueprint | live | HH:MM UTC | — | baseline |
| Muse | synthesized | — | context window constraint | -1 level |
| Sterling | deferred | — | out of scope | N/A — output absent |
| Ward | live | HH:MM UTC | — | baseline |
| Orbit | synthesized | — | blocking dependency | -1 level |
| Sage | synthesized | — | context window constraint | -1 level |

**Synthesis confidence adjustment:**
- Live agents: [list]
- Synthesized agents: [list + reason]
- Deferred agents: [list + reason]
- Ceiling applied: [HIGH / MEDIUM / LOW — per table above]
- Net effect: [plain-language summary of what this means for this session's decision quality]
```

---

## Example 1 — All-Live Session

All seven agents invoked via Agent tool. No ceiling applied.

```markdown
## Invocation Audit

| Agent | Method | Timestamp | Reason (if not live) | Confidence modifier |
|-------|--------|-----------|----------------------|---------------------|
| Atlas | live | 14:02 UTC | — | baseline |
| Blueprint | live | 14:05 UTC | — | baseline |
| Muse | live | 14:08 UTC | — | baseline |
| Sterling | live | 14:12 UTC | — | baseline |
| Ward | live | 14:15 UTC | — | baseline |
| Orbit | live | 14:18 UTC | — | baseline |
| Sage | live | 14:21 UTC | — | baseline |

**Synthesis confidence adjustment:**
- Live agents: Atlas, Blueprint, Muse, Sterling, Ward, Orbit, Sage
- Synthesized agents: None
- Deferred agents: None
- Ceiling applied: HIGH (no cap — all agents live)
- Net effect: Full council output. Synthesis confidence reflects actual agent quality, not modeling quality. This is the highest-fidelity session type.
```

---

## Example 2 — Mixed Live and Synthesized Session

Domain specialists live; peripheral agents synthesized due to context constraint. 4 agents synthesized — ceiling applies.

```markdown
## Invocation Audit

| Agent | Method | Timestamp | Reason (if not live) | Confidence modifier |
|-------|--------|-----------|----------------------|---------------------|
| Atlas | live | 09:30 UTC | — | baseline |
| Blueprint | live | 09:33 UTC | — | baseline |
| Ward | live | 09:37 UTC | — | baseline |
| Muse | synthesized | — | context window constraint | -1 level (HIGH→MEDIUM) |
| Sterling | synthesized | — | context window constraint | -1 level (HIGH→MEDIUM) |
| Orbit | synthesized | — | context window constraint | -1 level (HIGH→MEDIUM) |
| Sage | synthesized | — | context window constraint | -1 level (MEDIUM→LOW) |

**Synthesis confidence adjustment:**
- Live agents: Atlas, Blueprint, Ward
- Synthesized agents: Muse, Sterling, Orbit, Sage (context window constraint)
- Deferred agents: None
- Ceiling applied: MEDIUM (4 agents synthesized — 3+ threshold met)
- Net effect: Technical and legal voices are live and carry full weight. Financial (Sterling) and market (Orbit) voices are modeled — financial viability and GTM recommendations from this session should be re-validated with live Sterling/Orbit before irreversible commitments. Decision is suitable for reversible actions only under MEDIUM confidence ceiling.
```

---

## Example 3 — Fully Deferred / Minimal Session

Targeted session — only one agent relevant. All others deferred. No confidence ceiling penalty because deferred agents were genuinely out of scope.

```markdown
## Invocation Audit

| Agent | Method | Timestamp | Reason (if not live) | Confidence modifier |
|-------|--------|-----------|----------------------|---------------------|
| Atlas | live | 11:15 UTC | — | baseline |
| Blueprint | live | 11:17 UTC | — | baseline |
| Muse | deferred | — | out of scope (technical feasibility question) | N/A |
| Sterling | deferred | — | out of scope (no cost implication >$10K) | N/A |
| Ward | deferred | — | out of scope (no legal surface area) | N/A |
| Orbit | deferred | — | out of scope (no GTM component) | N/A |
| Sage | deferred | — | out of scope (targeted technical session) | N/A |

**Synthesis confidence adjustment:**
- Live agents: Atlas, Blueprint
- Synthesized agents: None
- Deferred agents: Muse, Sterling, Ward, Orbit, Sage (all: out of scope)
- Ceiling applied: HIGH (no cap — deferred agents were genuinely out of scope, not missing voices)
- Net effect: Targeted session. Confidence ceiling does not apply when agents are deferred because the domain doesn't require them. If scope expands into financial or legal territory, this session log must be updated or a new session initiated.
```

**Important distinction:** Deferred agents that are *out of scope* do not trigger the confidence ceiling. Deferred agents that are *in scope but not consulted* (e.g., "we should have asked Sterling but ran out of time") are recorded as `synthesized` with reason `time constraint` — because Atlas will have modeled them internally regardless.

---

## Audit Review Protocol

At the monthly calibration session (see `memory-protocol.md`):

1. Open all session logs from the past month
2. Review invocation audit sections
3. Check: were synthesized voices ever later validated by live invocation? If yes, did the live output materially differ?
4. Log fidelity gaps in `shared-knowledge/calibration/agent-accuracy.md` under the heading `Synthesis Fidelity`
5. If synthesized outputs consistently differ from live outputs for a given agent, note this in that agent's MEMORY.md under `Calibration Notes`

---

## Reference

This protocol is referenced by:
- `memory-protocol.md` — Session Log Format section
- `output-standards.md` — Atlas synthesis output requirements

Last updated: 2026-03-04

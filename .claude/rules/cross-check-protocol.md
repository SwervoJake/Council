# Cross-Check Protocol

All agents use standardized flags to trigger cross-agent review. Embed these flags directly in any output where they apply.

---

## Flag Reference

| Flag | Syntax | Meaning |
|------|--------|---------|
| Cross-check request | `[CROSS-CHECK: AGENT]` | Request review from the named agent |
| Urgent escalation | `[ESCALATE: AGENT]` | Urgent — requires immediate attention from named agent |
| Conflict documentation | `[CONFLICT: A vs B]` | Document disagreement for Atlas synthesis |
| Consensus signal | `[CONSENSUS: AGENTS]` | Multiple agents agree — increases confidence |
| Dependency block | `[DEPENDS: AGENT]` | Blocked until named agent provides input |
| External escalation | `[ESCALATE: EXTERNAL]` | Requires human expert or licensed professional |
| Rest advisory | `[SAGE: REST]` | Recovery protocol recommended before next session |
| Defer advisory | `[SAGE: DEFER]` | Sleep on this decision — quality will improve |
| Load advisory | `[SAGE: LOAD]` | Cognitive/stress load too high for clear thinking |
| Check-in advisory | `[SAGE: CHECK-IN]` | Wellbeing check warranted before proceeding |

---

## Usage Guidance

### CROSS-CHECK
Use when your domain expertise is insufficient to fully evaluate an aspect of the task. Name the specific agent whose lens is needed.

```
[CROSS-CHECK: STERLING] — Cost model needed before architecture decision is final.
[CROSS-CHECK: WARD] — Privacy implications of this data architecture require legal review.
[CROSS-CHECK: BLUEPRINT] — Technical feasibility of this timeline needs validation.
```

### ESCALATE: AGENT
Use when a finding requires immediate attention — not routine review. The named agent should be next to respond before the task moves forward.

```
[ESCALATE: ATLAS] — This decision cannot proceed without full synthesis.
[ESCALATE: WARD] — Material legal risk discovered mid-analysis.
```

### CONFLICT: A vs B
Use when two agents have reached genuinely incompatible conclusions. Atlas uses this to trigger a structured synthesis or debate.

```
[CONFLICT: STERLING vs BLUEPRINT] — Sterling's 18-month payback conflicts with Blueprint's 36-month build estimate.
```

### CONSENSUS: AGENTS
Use when multiple agents independently reached the same conclusion — this is a high-confidence signal Atlas should weight heavily.

```
[CONSENSUS: STERLING + WARD + ORBIT] — All three independently recommend deferring the enterprise tier launch.
```

### DEPENDS: AGENT
Use when your output is blocked — you cannot complete your analysis without named agent's input. Atlas routes accordingly.

```
[DEPENDS: STERLING] — Cannot assess regulatory risk without knowing the proposed pricing structure.
```

### ESCALATE: EXTERNAL
Use when a question requires a licensed professional (lawyer, doctor, CPA, etc.). Ward uses this most frequently; Sage uses it for medical questions.

```
[ESCALATE: EXTERNAL] — This contract structure requires review by a licensed attorney before signing.
[ESCALATE: PROFESSIONAL] (Sage variant) — Symptom pattern warrants physician evaluation.
```

### SAGE Flags
Sage flags are advisory, not commands. They invite the operator to reflect, not obey. Any agent may embed a Sage flag if they observe signals in session content.

```
[SAGE: LOAD] — This session has covered 6 high-stakes decisions. Decision quality risk is elevated.
[SAGE: DEFER] — This is irreversible and it's late in the session. Sleep on it.
```

---

## Flag Handling by Atlas

When Atlas encounters a flag:

| Flag Type | Atlas Action |
|-----------|-------------|
| `[CROSS-CHECK]` | Routes to named agent before synthesis |
| `[ESCALATE: AGENT]` | Named agent becomes next priority |
| `[CONFLICT]` | Triggers structured synthesis or debate |
| `[CONSENSUS]` | Raises confidence weight in synthesis |
| `[DEPENDS]` | Blocks synthesis until dependency resolved |
| `[ESCALATE: EXTERNAL]` | Pauses on that component; flags for human |
| `[SAGE: *]` | Acknowledges in synthesis; may pause session |

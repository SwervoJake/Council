# ADR-001: Council Routing Structure Audit
**Date:** 2026-03-04
**Status:** Accepted
**Deciders:** Blueprint
**Session:** 2026-03-04-council-deployment.md

---

## Context

The council's routing infrastructure was deployed in the 2026-03-04 memory system deployment session. This ADR records the post-deployment audit of the routing structure against the specification in `CLAUDE.md` and `factory_council_architecture.md`. The audit was conducted by Blueprint as part of implementing the Invocation Audit Protocol (Optimal fix).

---

## Audit Findings

### 1. Directory Structure

| Path | Expected | Status | Notes |
|------|----------|--------|-------|
| `/home/user/Council/.claude/agents/` | 7 agent definition files | PASS | All 7 files present |
| `/home/user/Council/workspace-ceo/` | Atlas workspace | PASS | Exists |
| `/home/user/Council/workspace-engineer/` | Blueprint workspace | PASS | Exists |
| `/home/user/Council/workspace-creative/` | Muse workspace | PASS | Exists |
| `/home/user/Council/workspace-finance/` | Sterling workspace | PASS | Exists |
| `/home/user/Council/workspace-legal/` | Ward workspace | PASS | Exists |
| `/home/user/Council/workspace-marketing/` | Orbit workspace | PASS | Exists |
| `/home/user/Council/workspace-health/` | Sage workspace | PASS | Exists |
| `/home/user/Council/shared-knowledge/` | Central knowledge store | PASS | Exists with all subdirectories |
| `/home/user/Council/logs/` | Session logs directory | PASS | Exists with handoffs/ and debates/ subdirs |

### 2. Agent Definition Files

| File | Status | Notes |
|------|--------|-------|
| `.claude/agents/atlas.md` | PASS | YAML frontmatter valid; description field present; tools include Task |
| `.claude/agents/blueprint.md` | PASS | YAML frontmatter valid; description field present |
| `.claude/agents/muse.md` | PASS | YAML frontmatter valid; description field present |
| `.claude/agents/sterling.md` | PASS | YAML frontmatter valid; description field present |
| `.claude/agents/ward.md` | PASS | YAML frontmatter valid; description field present |
| `.claude/agents/orbit.md` | PASS | YAML frontmatter valid; description field present |
| `.claude/agents/sage.md` | PASS | YAML frontmatter valid; description field present |

All 7 agents have `memory: project` — correct. All agents have `model: sonnet` — correct.

Tool access is appropriately differentiated:
- Atlas: `Read, Write, Edit, Bash, Grep, Glob, Task` — Task tool required for multi-agent orchestration
- Blueprint: `Read, Write, Edit, Bash, Grep, Glob` — Bash access for filesystem/build operations
- Sterling, Ward, Muse, Orbit, Sage: `Read, Write, Edit, Grep, Glob` — no Bash; appropriate for advisory roles

### 3. Memory Infrastructure

| Path | Expected | Status | Notes |
|------|----------|--------|-------|
| `workspace-ceo/CLAUDE.md` | Agent identity + @-import | PASS | Present; @-imports atlas_framework.md and COUNCIL_STATE.md |
| `workspace-engineer/CLAUDE.md` | Agent identity + @-import | PASS | Present; @-imports blueprint_framework.md |
| `workspace-creative/CLAUDE.md` | Agent identity + @-import | PASS | Present |
| `workspace-finance/CLAUDE.md` | Agent identity + @-import | PASS | Present |
| `workspace-legal/CLAUDE.md` | Agent identity + @-import | PASS | Present |
| `workspace-marketing/CLAUDE.md` | Agent identity + @-import | PASS | Present |
| `workspace-health/CLAUDE.md` | Agent identity + @-import | PASS | Present |
| `workspace-*/memory/MEMORY.md` | Session index in all 7 workspaces | PASS | All 7 present |
| `workspace-*/memory/` subdirs | Agent-specific pattern files | PASS | All 7 workspaces have populated memory subdirectories |

One gap corrected during this audit:

`workspace-engineer/CLAUDE.md` and `workspace-engineer/memory/MEMORY.md` both referenced `architecture-review-template.md` as an available template. The file does not exist in `workspace-engineer/templates/`. This was a dead reference — the template was listed in `blueprint_framework.md`'s Part 8 but was not created during Phase 2 deployment.

**Resolution:** Removed the ghost reference from both `workspace-engineer/CLAUDE.md` and `workspace-engineer/memory/MEMORY.md`. The three templates that do exist (`adr-template.md`, `cost-estimate-template.md`, `tradeoff-matrix-template.md`) are sufficient for current operation. The architecture-review template can be created if a complex review session warrants it.

**Tech debt classification:** Class B (Tactical) — ghost reference in documentation, not a functional failure. Low priority.

### 4. Central Knowledge Layer

| Path | Expected | Status | Notes |
|------|----------|--------|-------|
| `shared-knowledge/COUNCIL_STATE.md` | Company context + active questions | PASS | Populated from operator intake session 2026-03-04 |
| `shared-knowledge/decisions/active/` | Active decisions directory | PASS | Exists; currently empty (correct for new deployment) |
| `shared-knowledge/decisions/archived/` | Archived decisions directory | PASS | Exists; currently empty (correct) |
| `shared-knowledge/calibration/agent-accuracy.md` | Prediction tracking table | PASS | Exists with initialized tracking structure |
| `shared-knowledge/strategies/` | 6 domain strategy files | PASS | All 6 present: financial, technical, market, legal, creative, health patterns — each seeded at 0.5 confidence |
| `shared-knowledge/STRATEGY_INDEX.md` | N/A | NOT PRESENT | Spec does not require this file; absence is not a gap |

### 5. Routing Matrix Alignment

The routing matrix in `CLAUDE.md` specifies:

| Domain | Specified agents | Agent file description covers domain | Status |
|--------|-----------------|--------------------------------------|--------|
| Technical architecture | Blueprint | Yes — "technical feasibility assessment, system architecture design, technical debt evaluation..." | PASS |
| Financial analysis | Sterling | Yes — "financial modeling, ROI analysis, burn rate impact assessment..." | PASS |
| Legal/risk | Ward | Yes — "legal risk assessment, regulatory compliance review, IP protection, contract evaluation..." | PASS |
| Creative strategy | Muse | Yes — "idea generation, creative direction, brand narrative, campaign concepting..." | PASS |
| Go-to-market | Orbit | Yes — "go-to-market strategy, positioning, customer persona development, channel selection..." | PASS |
| Health/performance | Sage | Yes — "cognitive load assessment, burnout risk evaluation, decision fatigue monitoring..." | PASS |
| Product strategy | Blueprint + Muse + Orbit | All three have description fields that collectively cover product strategy | PASS |
| Full council | All agents | All 7 present | PASS |

**Routing mechanism:** Claude Code uses the `description` field in each `.claude/agents/[name].md` YAML frontmatter to determine which agent to invoke for a given task. All 7 description fields are substantive (8–12 lines each) and accurately describe their domains. The routing is sound.

**Spot-check — invocability test queries:**

The following queries would correctly route to the named agents based on description field matching:
- "Evaluate the technical feasibility of building a Slack bot on Railway" → Blueprint (technical feasibility, system architecture)
- "Model three scenarios for a $0 infrastructure business at pre-revenue stage" → Sterling (financial modeling, three-scenario, burn rate)
- "What are the legal risks of publishing AI-generated content under my name?" → Ward (legal risk assessment, IP protection, content liability)

### 6. Configuration

| Item | Expected | Status | Notes |
|------|----------|--------|-------|
| `.claude/settings.json` | CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS: "1" | PASS | Confirmed |
| `.claude/settings.json` | Task tool in permissions | PASS | `["Read", "Write", "Edit", "Bash", "Grep", "Glob", "Task"]` |
| `.claude/rules/cross-check-protocol.md` | Cross-check flag definitions | PASS | Present |
| `.claude/rules/output-standards.md` | Output format requirements | PASS | Present |
| `.claude/rules/memory-protocol.md` | Session closure protocol | PASS | Present; updated to include invocation audit reference and inline block |
| `.claude/rules/invocation-audit-protocol.md` | Invocation audit schema | PASS | Present; fully specified with examples and scoring rules |

---

## Decision

Routing structure is sound and operational. The council can function as specified with the following notes:

1. All 7 agents are correctly defined and will route correctly for their domains.
2. Atlas is the only agent with Task tool access — correct; Task enables multi-agent orchestration.
3. The one ghost reference (architecture-review-template.md) has been corrected.
4. No blocking gaps found.

---

## Tradeoffs Accepted

- `workspace-health/` does not have a `templates/` subdirectory (it has `protocols/` instead). This matches the Sage workspace design intention — Sage's outputs are protocols, not templates. Not a gap.
- `shared-knowledge/decisions/active/` and `archived/` contain only `.gitkeep` files. This is correct state for a newly deployed system with no decided questions yet.
- The `architecture-review-template.md` was listed in the framework specification (`blueprint_framework.md` Part 8) but was not created during Phase 2 deployment. The three existing templates cover current operational needs. Creating the missing template is Class B debt.

---

## Consequences

Expected: Council routes correctly from day one. No architectural rework needed.

Accepted negative: One Class B debt item (missing architecture-review-template). Low priority.

Risks to monitor: As session volume grows, verify that `memory: project` scope correctly loads workspace CLAUDE.md context when agents are invoked from the project root vs. from within their workspace subdirectory.

---

## Review Date

2026-09-04 (6 months) — or after 10 real council sessions, whichever comes first.

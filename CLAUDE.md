# CLAUDE.md — The Factory Council

This file is the primary reference for any AI assistant working in this repository. It describes the project's purpose, structure, conventions, and operational protocols.

---

## What This Repository Is

**The Factory Council** is a cognitive operating system — a multi-agent advisory board framework built entirely on Claude AI, Claude Code, and markdown files. It defines seven specialized AI agents that collaborate to provide strategic decision-making support across engineering, finance, creative, legal, growth, and health domains.

This repository contains the **complete framework documentation** for the system: agent identity schemas, operating methodologies, architecture specifications, memory protocols, and deployment guides. It is a documentation-first project — there is no application code, no build pipeline, and no test suite.

The system runs on:
- **Markdown files** as persistent storage and agent memory
- **Claude AI** (Sonnet model) as the reasoning engine
- **Claude Code** for subagent definitions and memory management via CLAUDE.md files
- **Cowork** (Anthropic) for folder-based agent activation and session scheduling
- **File system structure** as the bridge between agents and sessions

---

## Repository Structure

```
/Council/
├── CLAUDE.md                          # This file — AI assistant reference
├── README.md                          # Project overview and agent roster
├── factory_council_summary.md         # Executive summary (mirrors README)
├── factory_council_architecture.md    # Complete system architecture (master reference)
├── atlas_framework.md                 # CEO / Orchestrator agent methodology
├── blueprint_framework.md             # Chief Engineering Architect methodology
├── muse_framework.md                  # Chief Creative Strategist methodology
├── sterling_framework.md              # Chief Financial Strategist methodology
├── ward_framework.md                  # Risk & Legal Advisor methodology
├── orbit_framework.md                 # Growth & Marketing Strategist methodology
└── .git/
```

**Key file to read first:** `factory_council_architecture.md` — it contains all agent identity schemas (YAML), the cross-agent communication protocol, memory architecture, folder structure specification, Cowork configuration templates, and the 90-minute bootstrap guide.

---

## The Seven Agents

| Agent | Role | Governing Philosophy | Workspace |
|-------|------|---------------------|-----------|
| **Atlas** | CEO / Orchestrator | Adaptive Orchestration / Integrative Thinking | `/council/workspace-ceo/` |
| **Blueprint** | Chief Engineering Architect | Mathematical Determinism / Kaizen | `/council/workspace-engineer/` |
| **Muse** | Chief Creative Strategist | Divergent-Convergent Thinking / First Principles | `/council/workspace-creative/` |
| **Sterling** | Chief Financial Strategist | Expected Value Optimization / Margin of Safety | `/council/workspace-finance/` |
| **Ward** | Risk & Legal Advisor | Prudential Risk Management / Informed Consent | `/council/workspace-legal/` |
| **Orbit** | Growth & Marketing Strategist | Growth Loop Thinking / Jobs-to-be-Done | `/council/workspace-marketing/` |
| **Sage** | Health & Wellbeing Advisor | Allostatic Balance / Sustainable Performance | `/council/workspace-health/` |

### Agent Summaries

**Atlas** is the only agent authorized to make final calls and override individual recommendations. Atlas routes tasks, selects execution modes, synthesizes multi-agent outputs, resolves conflicts, and maintains the shared knowledge base. It does not execute — it coordinates.

**Blueprint** evaluates technical feasibility with PERT-calibrated timelines and confidence intervals. Every recommendation includes three options, a complexity score, and explicit technical debt classification. Cross-checks with Sterling and Orbit.

**Muse** operates in two gears: diverge wide (no filtering, pure expansion), then converge with ruthless curation. Every idea set ends with a wildcard — the highest-imagination option that deliberately breaks the brief. Cross-checks with Blueprint and Orbit.

**Sterling** requires a three-scenario model (best/base/worst), kill criteria, and burn rate impact assessment before any initiative proceeds. Speaks in numbers, margins, and cash flow. Cross-checks with Blueprint, Orbit, and Ward.

**Ward** classifies every risk as RED / AMBER / GREEN with a governing legal principle and specific mitigation path. Distinguishes what needs a lawyer from what needs awareness. Cross-checks with Sterling and Atlas.

**Orbit** frames every strategy with a Jobs-to-be-Done persona, a positioning statement, channel unit economics, and a measurement framework with leading and lagging indicators. Cross-checks with Muse, Sterling, and Blueprint.

**Sage** monitors the human operator — not the business — for cognitive fatigue, stress load, and recovery needs. Reads stress signals across council sessions. The only agent whose mandate is the person running the system, not the system's outputs.

---

## Cross-Agent Communication Protocol

Agents embed standardized flags in any output to trigger cross-agent review:

| Flag | Meaning |
|------|---------|
| `[CROSS-CHECK: AGENT]` | Request review from the named agent |
| `[ESCALATE: AGENT]` | Urgent — requires immediate attention |
| `[CONFLICT: A vs B]` | Document disagreement for Atlas synthesis |
| `[CONSENSUS: AGENTS]` | Multiple agents agree — increases confidence |
| `[DEPENDS: AGENT]` | Blocked until named agent provides input |
| `[ESCALATE: EXTERNAL]` | Requires a human expert or licensed professional |
| `[SAGE: REST]` | Recovery protocol recommended before next session |
| `[SAGE: DEFER]` | Sleep on this decision — quality will improve |
| `[SAGE: LOAD]` | Cognitive/stress load too high for clear thinking |
| `[SAGE: CHECK-IN]` | Wellbeing check warranted before proceeding |

### Debate Protocol (3 Rounds)

Used for high-stakes decisions with genuine uncertainty:

1. **Round 1 — Independent Position Papers** (parallel, no anchoring): Each agent states its stance, core argument, key evidence, assumptions, risk rating, and confidence level.
2. **Round 2 — Critique & Rebuttal** (sequential, all Round 1 visible): Each agent critiques the strongest opposing argument, rebuts with evidence, identifies gaps, and notes if their position changed.
3. **Round 3 — Atlas Synthesis**: Atlas delivers the decision, confidence level, reversibility classification, which agent's argument prevailed and why, acknowledged dissent, adopted risk mitigations, kill criteria, and a knowledge base update.

---

## Execution Modes

Atlas selects the appropriate mode based on task complexity and stakes:

| Mode | When to Use | Description |
|------|-------------|-------------|
| **Targeted** | Simple, domain-specific questions | 1–2 agents respond |
| **Parallel Council** | Complex multi-domain questions | 2–5 agents respond independently → Atlas synthesizes |
| **Sequential Pipeline** | Dependent analyses | Agent A → Agent B → Agent C, each building on prior output |
| **Debate** | High-stakes, genuinely uncertain decisions | Structured 3-round debate → Atlas judges |
| **Review** | Quality validation | One agent produces → another critiques → iterate |

---

## Memory Architecture (Three Tiers)

### Tier 1 — Working Memory (Claude Built-in)
Persistent facts about the user: name, role, company, stage, current projects, preferences, key context. Auto-loads every session. Example: "Series B fintech, $180K/month burn, 14 months runway."

### Tier 2 — Episodic Memory (CLAUDE.md + Markdown Journals)
- **Agent CLAUDE.md files**: Each agent's workspace has a CLAUDE.md carrying identity schema and operating methodology (slow-changing, authoritative)
- **Session logs**: `logs/YYYY-MM-DD-[topic].md` capturing each session's metadata, agent outputs summary, Atlas synthesis, decisions, and action items

**Session log format:**
```markdown
# /council/logs/YYYY-MM-DD-[topic].md
## Metadata
- Task: [description]
- Execution mode: [parallel/sequential/debate/targeted]
- Agents activated: [list]
## Agent Outputs Summary
### [Agent]
- Key recommendation
- Confidence level
- Cross-check flags raised
## Atlas Synthesis
- Decision: [statement]
- Rationale: [which agent's argument prevailed and why]
- Kill criteria: [numeric thresholds]
- Action items: [list]
```

### Tier 3 — Strategy Memory (Procedural Wisdom)
Transferable patterns stored with confidence scores in `shared-knowledge/strategies/[domain].md`.

**Confidence score rules:**
- Starts at 0.5
- +0.05 per successful application
- -0.10 per failure (asymmetric — prevents overconfidence)
- Above **0.80** → promoted to `COUNCIL_STATE.md` as established doctrine
- Below **0.30** → archived with failure postmortem

---

## Output Standards

Every agent output must include:
- **Confidence level:** HIGH / MEDIUM / LOW on every recommendation
- **Risk rating:** RED / AMBER / GREEN on every risk assessment
- **Back-of-envelope calculation** in any output containing financial claims
- **Self-assessment** at the end of each session (agent-specific format)

Atlas synthesis outputs additionally require:
- Reversibility classification (easily / partially / irreversible)
- Kill criteria with numeric thresholds
- Explicit acknowledgment of dissenting positions
- Knowledge base update entry

---

## Routing Matrix (Atlas Reference)

When Atlas receives a task, it routes to agents based on domain:

| Domain | Agents |
|--------|--------|
| Technical architecture | Blueprint |
| Creative strategy | Muse |
| Financial analysis | Sterling |
| Legal / risk | Ward |
| Go-to-market | Orbit |
| Health / performance | Sage |
| Product strategy | Blueprint, Muse, Orbit |
| Fundraising | Sterling, Ward, Orbit |
| Partnerships | Ward, Sterling, Orbit |
| Full council | Blueprint, Muse, Sterling, Ward, Orbit, Sage |

---

## Proposed Directory Structure (Not Yet Implemented)

The architecture specifies this folder layout for when the system is deployed. This repository currently contains only the framework documentation files — the structure below must be created during bootstrap:

```
/council/
├── CLAUDE.md                          # Council operating system
├── .claude/
│   ├── agents/                        # Subagent definition files
│   │   ├── atlas.md
│   │   ├── blueprint.md
│   │   ├── muse.md
│   │   ├── sterling.md
│   │   ├── ward.md
│   │   ├── orbit.md
│   │   └── sage.md
│   ├── rules/
│   │   ├── cross-check-protocol.md
│   │   ├── output-standards.md
│   │   └── memory-protocol.md
│   └── settings.json
├── workspace-ceo/          # Atlas workspace
│   ├── CLAUDE.md
│   ├── memory/
│   └── templates/
├── workspace-engineer/     # Blueprint workspace
├── workspace-creative/     # Muse workspace
├── workspace-finance/      # Sterling workspace
├── workspace-legal/        # Ward workspace
├── workspace-marketing/    # Orbit workspace
├── workspace-health/       # Sage workspace
├── shared-knowledge/
│   ├── COUNCIL_STATE.md    # Central state: stage, runway, active questions
│   ├── strategies/         # Domain pattern libraries with confidence scores
│   │   ├── financial-patterns.md
│   │   ├── technical-patterns.md
│   │   ├── market-patterns.md
│   │   ├── legal-patterns.md
│   │   ├── creative-patterns.md
│   │   └── health-patterns.md
│   ├── decisions/
│   │   ├── active/
│   │   └── archived/
│   └── calibration/
│       └── agent-accuracy.md
└── logs/
    ├── handoffs/
    └── debates/
```

---

## Bootstrap Guide (90 Minutes)

To deploy the council from this documentation:

**Step 1 — Create directory structure (10 min)**
```bash
mkdir -p /council/{.claude/{agents,rules}}
mkdir -p /council/{workspace-ceo,workspace-engineer,workspace-creative}/{memory,templates}
mkdir -p /council/{workspace-finance,workspace-legal,workspace-marketing}/{memory,templates}
mkdir -p /council/workspace-health/{memory,protocols}
mkdir -p /council/{shared-knowledge/{strategies,decisions/{active,archived},calibration}}
mkdir -p /council/logs/{handoffs,debates}
```

**Step 2 — Create core CLAUDE.md files (20 min)**
Write `/council/CLAUDE.md` (council OS), `~/.claude/CLAUDE.md` (global), and each agent's workspace CLAUDE.md using the identity schemas in `factory_council_architecture.md` Section 1. Keep each file under 200 lines — use `@` imports for longer references.

**Step 3 — Create subagent files (15 min)**
Create `.claude/agents/[name].md` for each agent with YAML frontmatter:
```yaml
---
name: sterling
description: >
  Chief Financial Strategist. Use for financial modeling, ROI analysis,
  burn rate, pricing, fundraising, or any capital allocation question.
tools: Read, Write, Edit, Grep, Glob
model: sonnet
memory: project
---
[Identity schema content from factory_council_architecture.md]
```

**Step 4 — Initialize shared knowledge base (10 min)**
Create `/council/shared-knowledge/COUNCIL_STATE.md` with company context: stage, runway, team size, active strategic questions. Create empty strategy files in each domain subdirectory.

**Step 5 — Configure Cowork (10 min)**
Settings → Cowork → Global Instructions → paste the Factory Council Protocol from `factory_council_architecture.md` Section 5.

**Step 6 — Enable Claude Code Agent Teams (15 min)**
Create `/council/.claude/settings.json`:
```json
{
  "env": {
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
  },
  "permissions": {
    "allow": ["Read", "Write", "Edit", "Bash", "Grep", "Glob", "Task"]
  }
}
```

**Step 7 — First council session (10 min)**
Open Cowork in `/council/workspace-ceo/`. Present a real strategic question. Atlas classifies, routes, you collect agent outputs, Atlas synthesizes. Log the session.

---

## Scheduled Automation

Configure with `/schedule` in Cowork:

| Schedule | Task |
|----------|------|
| Weekly (Friday) | Strategy Digest — synthesize session logs, update COUNCIL_STATE.md |
| Monthly | Confidence Calibration — compare predictions to outcomes, update confidence scores, archive patterns below 0.30 |
| Weekly | Sage Health Check-in — review session load patterns, flag recovery recommendations |

---

## Key Design Principles

These principles govern the framework and should inform any modifications:

1. **No external infrastructure.** Everything runs on local files + Claude AI. No servers, no databases, no APIs to maintain.
2. **Compounding intelligence.** Every session makes future sessions sharper through the three-tier memory system.
3. **Asymmetric calibration.** Failures subtract 2× more than successes add (–0.10 vs +0.05). Prevents overconfidence.
4. **Explicit tradeoff naming.** Decisions document what was given up, not just what was gained. No false consensus.
5. **Kill criteria discipline.** Every initiative gets numeric reversal thresholds before it starts.
6. **Reversibility classification.** Execution mode and decision weight depend on ability to undo.
7. **Integrative thinking over compromise.** Atlas synthesis seeks third paths capturing both sides' benefits, not averages of conflicting positions.
8. **Health as strategy.** Sage treats the human operator as the system's most leveraged component. Cognitive load is a strategic variable.
9. **Confidence over confidence.** Every recommendation carries an explicit confidence level. Low confidence is information, not failure.

---

## Conventions for AI Assistants

When working in this repository:

- **Read `factory_council_architecture.md` first** before making any structural changes. It is the authoritative specification.
- **Do not create agent workspace folders** in this repository root — the folder structure belongs in the deployed `/council/` directory, not here.
- **Preserve agent voice.** Each agent has a distinct persona and communication style defined in its framework file. If editing framework files, maintain the voice.
- **Flag missing Sage framework.** If creating a `sage_framework.md`, model it on the existing `*_framework.md` files — each contains an identity schema (YAML), operating framework (5–8 parts), specific methodologies, self-assessment templates, and memory file structure.
- **Don't duplicate documentation.** `factory_council_summary.md` currently mirrors `README.md`. If one is updated, check whether the other also needs updating.
- **Session logs use ISO date prefix:** `YYYY-MM-DD-[topic].md`
- **Strategy confidence scores** are stored as decimals 0.0–1.0, never percentages.
- **Risk ratings** are always RED / AMBER / GREEN — no other classification system.
- **Confidence levels** on recommendations are always HIGH / MEDIUM / LOW — no percentages or scores at this tier.

---

## Git and Branch Conventions

- Main branch: `master`
- Development branches: `claude/[description]-[session-id]`
- Commit messages should be descriptive and reference the component being changed (e.g., "Add sterling_framework debt classification methodology")
- No build steps required — this is a pure documentation repository

---

*The Factory Council. Seven agents. One direction.*

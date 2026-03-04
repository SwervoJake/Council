# Blueprint — Tech Stack Context
*Current stack, versions, known constraints, architectural decisions already locked.*
**Last updated:** 2026-03-04 (intake baseline)

---

## Stack Snapshot

### Home Desktop (Primary Development Machine)
| Layer | Technology | Specs / Version | Blueprint Note |
|-------|-----------|-----------------|----------------|
| CPU | AMD Ryzen 5 5600X | 6-core / 12-thread · 4.6GHz boost | Solid single-thread performance. No bottleneck for local AI inference or dev work. |
| GPU | NVIDIA GeForce RTX 3060 Ti | 8GB GDDR6 · 4864 CUDA cores | **Significant capability often overlooked.** Can run quantized LLMs (7B comfortably, 13B with Q4 quantization). Enables local AI experimentation at zero marginal cost. |
| Motherboard | MSI MAG B550 Tomahawk | AM4 | Stable platform. |
| RAM | 16GB | DDR4 | Adequate for most tasks. Constraint for running large local models simultaneously with other apps. |
| Storage | 500GB SSD | — | **Constraint.** Local LLM models alone can consume 4–8GB each. Storage hygiene required. |
| OS | Windows | — | Most tools available. WSL2 available if Linux tooling needed. |

### Work Device
| Layer | Technology | Blueprint Note |
|-------|-----------|----------------|
| Device | HP Laptop (model unknown) | Separate environment from home. No shared file access. |
| Capability | Unknown | Assume limited. Claude.ai web interface is the only reliable tool here. |
| Key constraint | No home-to-work file bridge | Fragmented environment. Work done at work cannot easily continue at home without cloud sync or explicit file transfer. |

### AI / Development Platform
| Tool | Tier | Monthly Cost | Constraint |
|------|------|-------------|------------|
| Claude.ai Pro | Pro | $20/month | Usage-capped. Sessions end when limit is hit. No upgrade to Max planned. |
| Claude Code | Included in Pro | $0 marginal | Primary development tool for agentic/framework work. |
| Other AI platforms | Testing phase | $0 | Used for cross-validation. Not primary. |

---

## Known Constraints

**Hard constraints affecting all technical recommendations:**

1. **No cloud infrastructure.** Everything runs locally. No server, no database, no hosting budget. Solutions must work on local hardware or free-tier cloud services.
2. **Claude Pro usage cap.** Development sessions are bounded by token usage, not time. Blueprint must design systems that minimize per-session token consumption where possible (e.g., efficient CLAUDE.md files, targeted context loading).
3. **Solo operator, novice skill level.** No team. Jacob is a novice across all technical domains. All recommendations must be operable by one person learning as they go. Complexity Score ceiling: 4/10 for initial implementations. Grow from there.
4. **500GB SSD storage.** Already partially consumed by OS and existing files. Local model storage must be managed carefully.
5. **No Claude Max upgrade.** This is a locked constraint. Do not design systems that require it. Design within Pro limits.
6. **Platform fragmentation.** Home desktop vs. work laptop — these are not connected. Council work happens at home. Job work stays on the work laptop.

---

## Hidden Capability — RTX 3060 Ti

**This is the most underutilized asset in Jacob's stack.**

The RTX 3060 Ti with 8GB VRAM can run:
- **Ollama** — local LLM inference (free, offline, no usage caps)
- **7B parameter models** (Mistral 7B, LLaMA 3 8B) — comfortably in 4–5GB VRAM
- **13B parameter models** — with Q4 quantization (fits in ~7GB VRAM)
- **Stable Diffusion** — image generation locally

**Strategic implication:** For workloads that are burning Claude Pro usage on routine tasks, local models via Ollama could handle those tasks at $0/month with zero usage cap. This would extend the effective budget of the Claude Pro subscription to higher-value tasks only.

Blueprint recommendation (when relevant): Evaluate Ollama deployment on home desktop as a Claude usage extension strategy. Complexity: 2/10. No cost. Reversible.

---

## Performance Benchmarks

*Current baseline for any recommendation that touches infrastructure:*

- Inference speed (local, 7B Q4): ~20–40 tokens/second on RTX 3060 Ti
- Storage budget available for development: Unknown (depends on current usage)
- Network: Home internet assumed adequate — no constraints stated
- Multi-tasking: 16GB RAM is adequate; running local model + browser + Claude Code simultaneously is feasible but may require memory management

---

## Locked Decisions (Not Up for Debate)

| Decision | Rationale | Locked By |
|----------|-----------|-----------|
| Claude Pro (no Max upgrade) | Budget constraint | Operator decision |
| Local-first storage | No cloud budget | Financial constraint |
| Solo operation | No team available | Structural constraint |
| Windows OS (home) | Existing hardware | Sunk cost — not worth changing |

---

## Technical Debt Register

| Debt Item | Class | Impact | Notes |
|-----------|-------|--------|-------|
| Platform fragmentation (home vs. work) | Class B | MEDIUM | Work done on HP laptop cannot continue at home without manual transfer |
| Unused AI platform accounts / experiments | Class C | LOW | "Still need to clean up unused inventory" — Jacob's words |
| No cloud backup | Class B | MEDIUM | Local-only storage = single point of failure for all council memory |
| No version control on council memory files | Class A | HIGH | Git tracks framework files; session logs and memory could be lost if drive fails |

**Class A** = blocking future development · **Class B** = slows development · **Class C** = cosmetic / minor

**Blueprint priority:** Class A debt (no backup of memory files) should be addressed before the council accumulates significant session history. A free-tier GitHub private repo or even a USB backup protocol would close this. Cost: $0. Effort: 1/10. Reversibility: easily reversible.

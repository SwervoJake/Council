# Sterling — Financial Models
*Active models with assumptions and last-updated dates. The living financial picture.*
**Last updated:** 2026-03-04 (intake baseline)

---

## Model 001 — Personal Income Baseline
**Updated:** 2026-03-04
**Purpose:** Establishes the financial floor every other model is anchored to. This is ground truth before any business exists.

### Inputs
| Line | Value | Basis |
|------|-------|-------|
| Hourly wage | $19.25 | Stated (intake) |
| Hours/week | 40 | Stated (intake) |
| Weekly gross | $770.00 | $19.25 × 40 |
| Annual gross | $40,040.00 | $770 × 52 |

### Tax Derivation (2025 estimates, single filer, KY)
| Tax | Rate | Amount/Year | Basis |
|-----|------|-------------|-------|
| Federal income | ~7.0% effective | ~$2,821 | Standard deduction $14,600; $25,440 taxable; 10%/12% brackets |
| FICA (SS + Medicare) | 7.65% | $3,063 | On gross |
| KY state income | 4.5% flat | $1,802 | KY flat rate on gross |
| **Total taxes** | **~19.2%** | **~$7,686** | — |

### Net Output
| Metric | Value | Notes |
|--------|-------|-------|
| Annual net | ~$32,354 | Gross minus taxes |
| **Monthly net take-home** | **~$2,696** | Primary budget constraint |
| Weekly net | ~$623 | — |

**Sensitivity:** Kentucky state tax is a flat rate — not sensitive to income level. Federal bracket is the one variable; a raise could push marginal rate to 22%, reducing net ~$17/month per $1K raise. Immaterial at this stage.

**Key assumption:** No pre-tax deductions (401k, health insurance, FSA). If Toyota Tsusho offers benefits with pre-tax deductions, actual take-home may differ. Verify against pay stub.

### Critical Constraint
- **Cash on hand at intake:** $85
- Monthly expenses: **unknown — not yet tracked**
- Monthly infrastructure cost: $20 (Claude Pro — only known fixed cost)
- **Available for savings/investment:** Unknown. Sterling cannot model savings capacity until monthly expenses are tracked.

**Immediate Sterling recommendation:** Track all expenses for one full pay cycle (two weeks minimum). This is the single most important financial action before any business decision is made.

---

## Model 002 — Business Viability on $0 Budget
**Updated:** 2026-03-04
**Purpose:** What types of businesses can Jacob actually start given current constraints?

### Constraints Applied
- Upfront capital available: ~$0 (after baseline expenses — unknown)
- Monthly infrastructure budget: $0 additional (Claude Pro already paid)
- Technical capability: Novice
- Team: Solo
- Time available: Late-night window post-1AM + weekends
- AI tool: Claude.ai Pro (usage-capped, no upgrade)

### Three-Scenario Model: Business Building

**Best Case (probability: 15%)**
- Finds a concept that spreads organically (short-form video hits algorithm)
- First revenue within 60–90 days
- Revenue model: creator monetization, Patreon, digital product sales
- Month 3 revenue: $200–500
- Path: Lean into short-form video immediately, iterate on format weekly

**Base Case (probability: 55%)**
- 3–6 months of building before any revenue signal
- Validation comes from audience growth, not immediate monetization
- Month 6 revenue: $0–100 (early, or still pre-revenue)
- Revenue model emerges from what the audience responds to
- Path: Council defines direction → content prototype → post → measure

**Worst Case (probability: 30%)**
- 12+ months, no meaningful revenue
- Audience doesn't grow, concept doesn't resonate
- Financial impact: ~$240/year in sunk Claude Pro costs (already being paid regardless)
- Personal impact: Time spent, experience gained — not a total loss
- Kill criterion: If no audience signal (followers, engagement, saves) after 6 months of consistent output → pivot concept, not medium

### Zero-Budget Business Models (viable given constraints)
| Model | Infrastructure needed | Revenue mechanism | Fit |
|-------|----------------------|------------------|-----|
| Short-form content creator | Phone camera (owned) + Claude Pro | Creator fund, sponsorship, digital products | **HIGH** — matches stated direction |
| Prompt/AI workflow consulting | Claude Pro only | Per-project fees | MEDIUM — needs network |
| Reselling / arbitrage | $0 to start (online platforms) | Margin on resale | LOW — capital-constrained |
| Digital product (template, guide) | Claude Pro to create | One-time sales | MEDIUM — needs audience first |
| Newsletter / content publishing | Free tier tools (Substack, Beehiiv) | Sponsorship, paid tier | MEDIUM — long road |

**Sterling position:** Short-form video content creation is the highest-fit model given budget = $0 and the stated product direction. It requires no upfront spend, generates audience before revenue (audience is the asset), and Claude Pro can power the content strategy and scripting. Kill criteria must be set before starting.

### Kill Criteria (Business Concept)
- If audience signal (combined reach, engagement) does not exceed 500 meaningful interactions across first 90 days → revisit concept
- If time investment exceeds 10 hours/week for 6 months with no revenue path visible → scope down or pivot
- If Claude usage cap becomes a material blocker to output → evaluate Max upgrade as a business expense against projected revenue

---

## Archived Models

*(None yet — first models established at intake)*

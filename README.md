# Revenue Intelligence Economic Multiplier — CFO Bridge

An interactive capital-allocation instrument for estimating the pre-tax gross contribution multiple created by AI-enabled Revenue Intelligence workflows, with a CFO bridge to implied Year-1 ROIC and simplified multi-year NPV by industry profile.

**Live tool:** https://grikard.github.io/revenue-intelligence-calculator/

---

## What this is

A planning instrument for the conversation between a workflow sponsor, a CFO, and a CIO before AI capital is committed against a revenue-influencing workflow. The tool produces a gross contribution multiple, an implied Year-1 ROIC bridge, and a simplified NPV across a selected value duration. Industry profiles seed defensible starting assumptions for nine verticals:

- Consumer Goods
- Energy & Utilities
- Financial Services
- High Tech
- Life Sciences
- Manufacturing
- Media
- Mobility / Auto
- Oil & Gas

Each profile pre-populates revenue under influence, improvement rate, contribution margin, realization factor, all-in AI investment, recurring cost, tax rate, WACC, value duration, benefit growth, and adoption ramp.

## Adoption ramp to steady state

Enterprise AI deployments rarely capture full benefit in Year 1. Compliance review, advisor adoption, data quality discovery, workflow integration, and change management each compress early-year capture. The tool models this with a three-option ramp selector.

| Ramp | Year 1 | Year 2 | Year 3 | Year 4 | Year 5+ |
|---|---|---|---|---|---|
| 1-year | 100% | 100% | 100% | 100% | 100% |
| 3-year | 50% | 80% | 100% | 100% | 100% |
| 5-year | 30% | 55% | 75% | 90% | 100% |

The 1-year option is an upper-bound view — what the workflow looks like if everything works immediately. It is included for backward comparability and sensitivity, not as a planning case.

The 3-year ramp is the empirical typical for mainstream enterprise AI deployments. Default for Media, Manufacturing, High Tech, Consumer Goods, and Mobility / Auto.

The 5-year ramp is the regulated and deep-integration envelope. Default for Financial Services, Life Sciences, Energy & Utilities, and Oil & Gas.

Adoption ramp is multiplicative with the realization factor. The realization factor sets the steady-state ceiling (how much of the workflow's theoretical benefit is captured at maturity). The ramp sets the time-shape (how long until steady state). The two combine cleanly: Year-t benefit = Gross Contribution × Realization Factor × Ramp(t) × (1 + Growth)^(t-1).

## Two ROIC views

The tool reports two ROIC figures side by side in the headline metrics.

**Year-1 ROIC** reflects the selected adoption ramp and is the number that has to survive year-end actuals review. For a Financial Services workflow under the 5-year default ramp, this typically lands in the 10–20% band.

**Steady-state ROIC** is the asset's earning capability at maturity, with the ramp fully delivered and the realization factor holding. For the same Financial Services workflow, steady state typically lands in the 70–90% band.

Either figure alone is misleading. The spread between them is the conversation a CFO and a workflow sponsor need to have before capital is committed.

## What this is not

This is not accounting ROIC. Accounting ROIC requires NOPAT divided by invested capital under finance-approved definitions. The Year-1 ROIC the tool reports is an implied bridge from incremental NOPAT to initial AI investment, useful for screening, not for valuation. The NPV is a simplified FCF approximation that treats incremental FCF as approximately equal to incremental NOPAT and ignores working capital, incremental capex, and adoption ramp. Formal valuation should use production-measured inputs, finance-approved tax and WACC, working capital and capex modeling, and an explicit adoption curve.

## Usage

The artifact is a single static HTML file. Open it in any modern browser; no build step, no dependencies.

```bash
git clone https://github.com/grikard/revenue-intelligence-calculator.git
cd revenue-intelligence-calculator
open index.html
```

Click an industry profile to seed defaults. Adjust any of the ten levers to fit the workflow under evaluation. The tool recomputes on each input change.

## Core calculator formula

```text
Economic Multiplier =
  (Revenue Under Influence × Improvement Rate × Contribution Margin × Realization Factor)
  ÷ Initial AI Investment
```

## CFO bridge

```text
Incremental NOPAT_t = (Gross Contribution_t − Recurring AI Cost) × (1 − Tax Rate)

NPV = −I0 + Σ [Incremental FCF_t ÷ (1 + WACC)^t]
```

The tool assumes Incremental FCF ≈ Incremental NOPAT and applies the selected annual benefit growth rate to gross contribution. Year-1 benefit is modeled at full realization; production planning should overlay an explicit adoption ramp.

## Empirical foundation

The Workflow Economics thesis draws on Kim, Kim, and Koning, *Mapping AI Into Production* (INSEAD / Harvard Business School working paper, 2026), which documents AI-enabled revenue lift and capital demand reduction across commercial workflows. The realization factor in this tool is calibrated against the field-measured gap between pilot promise and production delivery in that work.

The bottleneck to enterprise AI value is discovering where AI creates value in production, not the technology itself. This tool is a sequencing instrument for that discovery, not a substitute for it.

## Interpretation discipline

Four practical guardrails sit alongside the calculator output.

The revenue denominator must reflect revenue actually influenced by the AI workflow, not total corporate revenue. The multiplier scales linearly with the denominator, so denominator discipline determines whether the output is meaningful or marketing.

The realization factor is where CFO skepticism should enter first. Adoption, data quality, workflow fit, change friction, and execution probability all sit inside this single number. Pilot-stage workflows should not be modeled above 60%.

Contribution margin should be incremental contribution margin after direct costs and variable GTM costs, not corporate gross margin. Using corporate gross margin as a proxy is acceptable only when documented and defensible.

ROIC reported by the tool is an implied bridge. Formal accounting ROIC requires finance-approved invested capital and NOPAT definitions and is computed separately.

The improvement rate slider extends to 8% to accommodate edge cases, but the production-validated empirical band on AI-enabled revenue lift sits closer to 0.5–3%. Avoid anchoring to the slider maximum.

## Roadmap

**Shipped in v3:** stale NPV placeholder fix, ARIA accessibility pass, expanded precision note covering FCF ≈ NOPAT approximation, on-page Kim/Kim/Koning empirical citation.

**Shipped in v4:** adoption ramp selector (1-year / 3-year / 5-year) with per-industry defaults, dual ROIC headline display (Year-1 and Steady-state), cumulative-cash-flow payback calculation that respects ramp curve.

**Planned for v5:** one-variable sensitivity tornado on the four highest-leverage inputs (revenue under influence, improvement rate, realization factor, contribution margin), CSV export of the multi-year cash flow schedule, URL hash encoding of input state for shareable scenarios.

**Under consideration:** side-by-side scenario comparison, separated software and implementation services cost, custom-curve ramp mode for analysts with production-measured adoption data, expanded industry profile library, print-friendly stylesheet for board-pack inclusion.

## License

MIT — see [LICENSE](./LICENSE).

## Author

**Gary Rikard, MBA** — Workflow Economics series.

LinkedIn: https://www.linkedin.com/in/garyrikard

## Suggested GitHub topics

```text
revenue-intelligence
workflow-economics
economic-multiplier
npv
roic
capital-allocation
enterprise-ai
gross-contribution
cfo
agentforce
```

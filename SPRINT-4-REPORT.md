# Sprint 4: Metrics Dictionary — Report

**Status:** Done
**Date:** 2026-04-15

## Goal

Page 05 — 18 metric cards with full details.

## Deliverables

### `pages/metrics.html` (39KB)

**18 metric cards across 5 categories:**

| Category | Metrics | Count |
|----------|---------|-------|
| Revenue | Turnover, GGR, GGR Margin, NGR, NGR Margin | 5 |
| Unit Economics | LTV, LTV:CAC, CAC, Payback Period | 4 |
| Players | Active Players (DAU/WAU/MAU), FTD Count, Retention D1/D7/D30, Churn Rate | 4 |
| Marketing | CPA/CPD, ROAS, Conversion Funnel | 3 |
| Product | Revenue Concentration, Bonus Cost Ratio | 2 |

**Each metric card includes:**
- Name + category badge
- Definition (1-2 sentences, plain language, iGaming context)
- Formula (mathematical notation)
- SQL example (5-10 lines, querying mart tables from Data Model)
- Benchmarks (EU / LatAm / SEA where applicable)
- Alert thresholds (red / yellow badges)
- Pitfalls (2-3 common interpretation errors)
- Owner (Product / Marketing / Finance)
- Dependencies (which other metrics it depends on)
- Dimensions (geo, channel, product, segment)

**SQL examples reference:**
- mart_daily_kpi, mart_player_lifetime, mart_cohort_analysis, mart_marketing_performance
- int_bets_enriched, fct_deposits
- ClickHouse-specific functions: toDate, toMonth, countIf, nullIf

**Cross-link:** Data Model (03)

## Checklist

- [x] 18 metric cards (5 Revenue + 4 Unit Economics + 4 Players + 3 Marketing + 2 Product)
- [x] Each card: definition, formula, SQL, benchmarks, alerts, pitfalls, owner, dependencies, dimensions
- [x] SQL examples query correct mart tables
- [x] Grouped by category with section headers
- [x] Navigation works (sidebar, breadcrumbs, prev/next)
- [x] No hardcoded colors
- [x] Page size 39KB (< 100KB target)

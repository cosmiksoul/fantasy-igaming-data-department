# Sprint 8: Dashboard Mockups — Report

**Status:** Done
**Date:** 2026-04-15

## Goal

Page 12 — 6 rich dashboard mockups with inline SVG charts, sparklines, and conditional formatting.

## Deliverables

### `pages/dashboards.html` (39KB)

**6 дашбордов с продвинутой визуализацией:**

| # | Dashboard | Визуальные элементы |
|---|-----------|-------------------|
| 1 | CEO Daily Pulse | 4 KPI cards с SVG sparklines (7 дней) + 30-day NGR line chart (SVG polyline с area fill) + geo hbars + Casino/Sports stacked bar |
| 2 | Marketing Performance | Визуальная воронка (Visit→Reg→FTD с процентами конверсии) + spend hbars по каналам + таблица с conditional formatting (LTV:CAC < 2 = красный, > 3 = зелёный) |
| 3 | Casino Product | GGR hbars по 5 провайдерам + CSS donut chart (Slots 65% / Live 25% / Table 10%) + таблица top-10 игр с RTP conditional formatting |
| 4 | Sports Product | Handle hbars по 5 лигам (с маржой %) + pre-match/live stacked bar + margin sparkline (30 дней) |
| 5 | Cohort Analysis | Retention heatmap (6 когорт × 7 месяцев, зелёный→жёлтый→красный) + cumulative NGR SVG multi-line chart (4 когорты, каждая своего цвета) |
| 6 | Data Health | 4 KPI cards (DQ Score со sparkline, SLA, P1, P2/P3) + mart status таблица со status dots (●) + SLA compliance bar chart по неделям |

**Визуальные компоненты (чистый CSS + inline SVG):**
- SVG sparklines (polyline + area fill, 80×32px) — 6 штук
- SVG line chart (polyline + grid + axis labels, 600×140px) — 2 штуки
- Horizontal bar charts (CSS) — 17 строк
- Stacked bars (CSS flexbox) — 2 штуки
- CSS donut chart (conic-gradient) — 1 штука
- Retention heatmap (inline background colors) — 42 ячейки
- Conditional formatting (cell-good/warn/bad) — таблицы Marketing + Casino + Data Health
- Status dots (green/yellow/red) — 5 штук

### CSS additions (`css/style.css`)

Расширенный набор dashboard компонентов:
- `.dash-sparkline`, `.spark-up`, `.spark-down`, `.spark-area` (SVG sparklines)
- `.dash-chart`, `.chart-line`, `.chart-area`, `.chart-grid`, `.chart-dot` (SVG charts)
- `.dash-hbar-*` (horizontal bar charts)
- `.dash-stacked`, `.dash-stacked-seg` (stacked bars)
- `.dash-funnel`, `.dash-funnel-conv` (воронки с конверсиями)
- `.dash-donut`, `.dash-donut-center`, `.dash-donut-legend` (CSS donut chart)
- `.cell-good`, `.cell-warn`, `.cell-bad`, `.cell-bg-*` (conditional formatting)
- `.status-dot.green/yellow/red` (status indicators)

## Checklist

- [x] CEO Daily Pulse: KPI cards + sparklines + 30-day line chart + geo bars + product split
- [x] Marketing: visual funnel + spend bars + conditional formatted channel table
- [x] Casino: provider bars + donut chart + top-10 games with RTP status
- [x] Sports: league bars + pre-match/live stacked + margin sparkline
- [x] Cohort: retention heatmap (colored cells) + cumulative NGR multi-line SVG chart
- [x] Data Health: KPI cards + sparkline + mart status with dots + SLA bar chart
- [x] Все charts — чистый CSS + inline SVG, без библиотек
- [x] Фейковые данные реалистичны для Fantasy iGaming ($5M NGR/мес, 500K MAU)
- [x] Navigation works
- [x] Page size 39KB (< 100KB)

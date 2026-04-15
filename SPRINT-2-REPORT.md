# Sprint 2: Org Structure — Report

**Status:** Done
**Date:** 2026-04-15

## Goal

Page 02 — org chart + stream details + RACI + skill matrix + career ladder.

## Deliverables

### `pages/org-structure.html` (31KB)

**Visual Org Chart (HTML/CSS):**
- Director of Data (top, purple border)
- 4 leads with team members below (color-coded per stream)
- Responsive: wraps on mobile, horizontal on desktop

**4 Stream Detail Accordions:**

| Stream | Lead + Team | Badge Color |
|--------|-------------|-------------|
| Data Engineering | 1 Lead + 2 DE + 1 AE + 1 Platform | blue |
| Analytics | 1 Lead + 3 Product + 2 Marketing + 1 Financial + 1 BI Dev | teal |
| Data Science | 1 Lead + 1 ML Engineer + 2 DS | pink |
| BI Engineering | 1 Lead + 1 BI Dev + 1 Data Literacy | amber |

Each stream accordion contains:
- Person cards with role + description (14 total)
- Responsibilities (bulleted list)
- Interactions (with which teams)
- Key deliverables with SLA targets

**RACI Matrix (HTML table):**
- 7 processes: new dashboard, new pipeline, new ML model, P1 incident, new metric, A/B test, governance review
- 5 columns: DE, Analytics, DS, BI Eng, Director

**Skill Matrix (HTML table):**
- 7 roles x 8 skills (SQL, Python, dbt, BI, Statistics, ML, Communication, Domain)
- Levels: expert (teal badge), proficient (blue), basic (gray)

**Career Ladder (timeline):**
- 5 levels: Junior → Middle → Senior → Lead → Head/Director
- Per level: expectations, scope of impact, time-on-level, management ratio

### CSS additions (`css/style.css`)

New `.org-chart` component styles:
- `.org-node`, `.org-node-director`, `.org-node-lead`
- `.org-connector`, `.org-row`, `.org-branch`
- `.org-team-list`, `.org-team-member`

## Checklist

- [x] Visual org chart (HTML/CSS, Director → 4 leads → teams)
- [x] 4 stream accordions with person cards, responsibilities, interactions, deliverables
- [x] RACI matrix (7 processes x 5 roles)
- [x] Skill matrix (7 roles x 8 skills with badge levels)
- [x] Career ladder (5 levels with timeline component)
- [x] Navigation works (sidebar, breadcrumbs, prev/next)
- [x] All accordions expand/collapse
- [x] No hardcoded colors
- [x] Page size 31KB (< 100KB target)
- [x] Content in Russian, code/classes in English

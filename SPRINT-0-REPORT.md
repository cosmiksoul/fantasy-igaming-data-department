# Sprint 0: Foundation — Report

**Status:** Done
**Date:** 2026-04-15

## Goal

Shared infrastructure, design system, working navigation.

## Deliverables

### `css/style.css` (22KB)

- CSS custom properties: colors, fonts, spacing, radii, transitions
- Dark theme (#0e0e11 body, #16161c cards)
- Typography: DM Sans (body) + JetBrains Mono (code) via Google Fonts CDN
- Mobile-first responsive: 375px base → 768px tablet → 1024px desktop
- Reusable components:
  - `.accordion` — collapsible sections (header + chevron + body)
  - `.tool-card` — stack tool (name, badge, description, alt, trade-off)
  - `.metric-card` — metric (name, definition, formula, SQL, benchmarks, pitfalls)
  - `.person-card` — role in org (role, name, description)
  - `.sla-table` — SLA matrix rows
  - `.timeline` / `.timeline-block` — roadmap timeline
  - `.badge` — colored pills (primary, teal, blue, amber, pink, red, green, coral, gray)
  - `.alert` — tip (green), warning (amber), info (blue), danger (red)
  - `.code-block` — code with language label, minimal CSS syntax highlighting
  - `.mermaid-block` — wrapper for mermaid.js diagrams
  - `.btn` — primary and ghost buttons (min 44px tap target)
  - `.card`, `.section-card` — generic and section grid cards
- Layout: sidebar (fixed desktop / slide-out mobile), burger, breadcrumbs, prev/next nav, footer

### `js/nav.js` (6KB)

- `NAV_SECTIONS` registry: 17 pages in 5 groups (Core, Governance, Operations, Practice, Advanced)
- `buildSidebar()` — renders sidebar with group titles, links, active page highlight
- `buildBreadcrumbs()` — generates `Fantasy iGaming > Section Name`
- `buildPrevNext()` — prev/next links at page bottom
- `initBurger()` — burger toggle, overlay, Escape key close
- `toggleAccordion()` — accordion open/close
- Path-aware: works from root (`index.html`) and from `/pages/` subdirectory

### `index.html` (13KB)

- Hero: title, subtitle, description, CTA → data-architecture.html
- Company card: product, markets, MAU, NGR, team size, stage, stack (responsive grid)
- Section grid: 17 cards (2-col desktop / 1-col mobile), color-coded border-left per category
- Disclaimer block
- Footer with license

### `pages/_template.html` + 17 placeholder pages

- Template: boilerplate with burger, sidebar, breadcrumbs, content area, prev/next, footer
- Generated pages: data-architecture, org-structure, data-model, event-taxonomy, metrics, data-governance, sla, dataops, mlops, data-lineage, incident-response, dashboards, ab-testing, management, onboarding, finops, roadmap
- Each page is standalone (direct URL access works)

## Checklist

- [x] `css/style.css` — design system, all components
- [x] `js/nav.js` — sidebar, burger, breadcrumbs, prev/next, accordion
- [x] `index.html` — hero, company card, section grid, disclaimer, footer
- [x] `pages/_template.html` — page boilerplate
- [x] 17 placeholder pages generated from template
- [x] Navigation works on mobile (burger + slide-out) and desktop (fixed sidebar)
- [x] Clicking section card → placeholder page with working nav
- [x] All files under 100KB target
- [x] No hardcoded colors — all from CSS variables
- [x] Mobile-first responsive (375px → 768px → 1024px)

## File Sizes

| File | Size |
|------|------|
| `css/style.css` | 22KB |
| `js/nav.js` | 6KB |
| `index.html` | 13KB |
| `pages/*.html` (each) | ~1.5KB |
| **Total** | ~67KB |

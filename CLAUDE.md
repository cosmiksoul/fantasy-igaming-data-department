# CLAUDE.md

## Project

Fantasy iGaming LTD — static multi-page site (GitHub Pages). Interactive reference for a fictional iGaming company's data function.

## Tech Stack

- Pure HTML/CSS/JS. No frameworks, no npm, no build tools.
- External CDN only: Google Fonts (DM Sans, JetBrains Mono), mermaid.js
- Each page < 100KB. Lighthouse > 95.

## File Structure

```
index.html              — main page (intro + section grid)
css/style.css           — ALL shared styles (theme, layout, components)
js/nav.js               — shared navigation logic (burger, sidebar, active state, prev/next)
pages/*.html            — one file per section (01-17)
assets/                 — images, og-image
```

## Rules

### General
- Language: Russian (content), English (code, comments, CSS classes, JS variables)
- Every page includes: shared CSS (`../css/style.css`), shared JS (`../js/nav.js`), navigation sidebar, breadcrumbs, prev/next links, footer
- All pages must work standalone (direct URL access), not just via navigation
- Mobile-first: design for 375px, then adapt to tablet/desktop
- Dark theme only (for now). All colors from design tokens in style.css. No hardcoded colors in page files.

### HTML
- Semantic HTML5: `<main>`, `<nav>`, `<section>`, `<article>`, `<aside>`
- No inline styles except rare dynamic values
- All interactive elements: accordion, tabs — must work without JS (CSS-only fallback) where possible
- Accordion sections start collapsed by default unless specified
- Every page has proper `<title>`, `<meta description>`, Open Graph tags

### CSS
- Single style.css for everything. No per-page CSS files.
- CSS custom properties (variables) for all colors, fonts, radii, spacing
- Mobile-first media queries: base = mobile, `@media (min-width: 768px)` for tablet, `@media (min-width: 1024px)` for desktop
- Class naming: BEM-like but simplified. `.section`, `.section-header`, `.section-body`. No deep nesting.
- Components are generic and reusable: `.card`, `.accordion`, `.tool-card`, `.metric-card`, `.alert`, `.code-block`, `.sla-row`, `.person-card`, `.timeline-block`

### JS
- Vanilla JS only. No libraries except mermaid.js.
- nav.js handles: burger toggle, sidebar active state, prev/next generation
- Per-page JS (if needed) goes in a `<script>` at bottom of that page, not in separate files
- Accordion toggle: simple class toggle, no animation libraries
- Mermaid diagrams: initialize on DOMContentLoaded, dark theme config

### Content
- Tone: professional but accessible. Not academic, not overly casual. Like explaining to a smart colleague.
- All examples are iGaming-specific (Fantasy iGaming LTD context)
- SQL examples: use table names from SPEC.md data model (stg_*, int_*, mart_*)
- Fake but realistic numbers: $5M NGR, 500K MAU, 3-5% casino hold, etc.
- Every tool/technology mention includes: what it does (1-2 sentences), why chosen, alternative, trade-off

### Component Patterns

**Accordion:**
```html
<div class="accordion">
  <div class="accordion-header" onclick="toggleAccordion(this)">
    <span class="accordion-chevron">▶</span>
    <span class="accordion-title">Title</span>
  </div>
  <div class="accordion-body">
    Content here
  </div>
</div>
```

**Tool card:**
```html
<div class="tool-card">
  <div class="tool-card-header">
    <span class="tool-card-name">ClickHouse</span>
    <span class="badge badge-primary">primary</span>
  </div>
  <p class="tool-card-desc">Description</p>
  <div class="tool-card-meta">
    <span class="tool-card-alt">Alt: BigQuery, Snowflake</span>
    <span class="tool-card-tradeoff">Trade-off: needs DE team for ops</span>
  </div>
</div>
```

**Metric card:**
```html
<div class="metric-card">
  <div class="metric-card-header">
    <span class="metric-card-name">NGR</span>
    <span class="badge badge-revenue">revenue</span>
  </div>
  <p class="metric-card-def">Net Gaming Revenue — what the business actually keeps.</p>
  <div class="metric-card-formula">GGR − Bonus Cost − Provider Fees − Payment Fees − Taxes</div>
  <div class="code-block">SELECT ... </div>
  <div class="metric-card-benchmarks">...</div>
  <div class="metric-card-pitfalls">...</div>
</div>
```

**Alert boxes:**
```html
<div class="alert alert-tip">Tip content</div>
<div class="alert alert-warning">Warning content</div>
<div class="alert alert-info">Info content</div>
```

**Code blocks:**
```html
<div class="code-block" data-lang="sql">
  <pre><code>SELECT date, SUM(bet_amount) as turnover FROM mart_daily_kpi GROUP BY date</code></pre>
</div>
```

## Build Order

Follow sprint plan in SPRINTS.md. Build shared infrastructure first (style.css, nav.js, index.html), then pages one by one. Each page should be fully functional before moving to next.

## Quality Checks

Before considering a page done:
1. Renders correctly on 375px mobile viewport
2. Navigation works (sidebar, breadcrumbs, prev/next)
3. All accordions expand/collapse
4. Mermaid diagrams render (if applicable)
5. No hardcoded colors — all from CSS variables
6. Content matches SPEC.md for that section
7. Code blocks have proper formatting
8. All links to other sections work

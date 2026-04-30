# Project Context: Satellite Quality Story

## Overview
Interactive data narrative (5-act story) revealing how shift timing impacts defect rates in satellite manufacturing. Connects to Apple Vision Pro engagement for AR quality inspection.

## Key Facts
- **Project:** P302 - Protogen Interactive Data Story
- **Tech Stack:** Vue 3 + TypeScript, Vite, Chart.js, GSAP
- **Story:** "Seeing in the Dark" — 3.2x higher defect rate on night shift
- **Timeline:** 7-day build (Day 1-7)
- **Deployment:** Vercel with password protection
- **Current Phase:** Phase 1 (setup complete), Phase 2 (base structure)

## Core Narrative (5 Acts)
1. **Act 1: The Problem** — $4.2M cost, 2,847 defects
2. **Act 2: The Surprise** — Night shift produces 57% of defects with 25% of volume
3. **Act 3: The Pattern** — Root causes: staffing, experience, lighting, process
4. **Act 4: The Impact** — Cost breakdown, correlations, customer impact
5. **Act 5: The Solution** — Best practices, pilot results (67% reduction), ROI calculator, AR future vision

## Design Specifications
- **Theme:** Dark aerospace/manufacturing aesthetic
- **Colors:** Deep blue (#0D1B2A) + cyan (#00D9FF), traffic light status colors
- **Typography:** Orbitron titles, Roboto body, Roboto Mono for data
- **Responsive:** Desktop (1200px+), Tablet (768-1199px), Mobile (<768px)
- **Animations:** GSAP scroll triggers, chart reveals, counter animations
- **Accessibility:** WCAG 2.1 AA, keyboard nav, screen readers, reduced-motion respect

## Project Structure
```
satellite-quality-story/
├── .claude/               # AI scaffolding
├── docs/                  # Documentation
├── src/
│   ├── components/        # Vue components
│   ├── composables/       # Reusable logic
│   ├── data/              # 9 JSON mock files
│   ├── views/             # Page components
│   ├── App.vue, main.ts
│   └── style.css
├── public/
├── BRIEF.md, README.md
└── package.json, vite.config.ts, tsconfig.json
```

## Data Files (9 Total)
All in `/src/data/`:
1. qualityOverview.json
2. defectsByShift.json
3. defectTypes.json
4. defectHeatmap.json
5. inspectorStats.json
6. costBreakdown.json
7. correlations.json
8. pilotResults.json
9. roiCalculator.json

## Components to Build
### Phase 2 (Base Structure)
- ScrollProgress ✓
- StorySection (wrapper)

### Phase 3 (Acts 1 & 2)
- AnimatedCounter
- CostBreakdown (card reveal)
- BarChart (Expected vs Actual)

### Phase 4 (Act 3)
- HeatMap (custom SVG)
- StackedBarChart (defect types)
- ComparisonCards (staffing, etc.)
- FilterButtons

### Phase 5 (Act 4)
- WaterfallChart
- ScatterPlot
- Timeline
- Tooltips

### Phase 6 (Act 5)
- BestPracticeCards
- BeforeAfterChart
- ARVisualization
- ROICalculator (sliders)

## Key Interactions
- Scroll-based animations (GSAP ScrollTrigger)
- Interactive filters (Act 3)
- Hover tooltips (charts)
- ROI calculator sliders with real-time updates
- Responsive breakpoints

## Accessibility Requirements
- WCAG 2.1 AA compliance
- Color contrast: 7:1 (AAA) for text
- Keyboard navigation, focus indicators
- ARIA labels on interactive elements
- Screen reader table for charts
- prefers-reduced-motion support
- Touch targets: 44px minimum

## Deployment Checklist
- [ ] Live on Vercel URL
- [ ] Password protected
- [ ] All 5 acts display correctly
- [ ] Scroll animations trigger properly
- [ ] Responsive design: desktop, tablet, mobile
- [ ] Accessibility audit passed
- [ ] No console errors
- [ ] Performance: <3s load, 60fps scroll

## Success Criteria (from BRIEF.md)
- First-time user understands top 3 insights
- Visualizations load quickly and work on desktop/mobile
- Narrative is self-explanatory
- Data sources and assumptions transparent
- Visual design fits aerospace industry
- Story arc is compelling and clear

## References
- BRIEF.md — Full narrative spec
- docs/design-decisions.md — Design rationale
- docs/data-dictionary.md — Data definitions
- Narrative arc: 5-act structure with clear problem/surprise/pattern/impact/solution

## Next Steps
1. Phase 1: ✓ Setup, BRIEF.md, data files created
2. Phase 2: Build story structure (StorySection component, base layout)
3. Phase 3: Act 1 & 2 (counter, cost breakdown, bar chart)
4. Continue phases 4-7 per build sequence

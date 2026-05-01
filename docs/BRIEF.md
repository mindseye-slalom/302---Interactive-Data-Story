# Project Brief: Seeing in the Dark

## Summary

This project is an interactive, scroll-based data story focused on quality variance across manufacturing shifts in satellite component production.

The narrative shows why defects cluster on night shift, what the operational root causes are, and which interventions deliver measurable ROI.

## Audience and Use

- Audience: quality leaders, operations stakeholders, and engineering managers.
- Use case: presentation-ready story for internal discussion and decision support.
- Primary form factor: desktop first, with responsive behavior for tablet and mobile.

## Current Narrative Structure (Implemented)

1. Act 1 - The Problem
2. Act 2 - The Surprise
3. Act 3 - The Root Causes
4. Act 4 - The Ripple Effect
5. Act 5 - The Path Forward

Each act is implemented in Vue and rendered as a section of a single-page narrative.

## Current Implementation State

### Architecture

- Framework: Vue 3 + TypeScript.
- Build system: Vite.
- Charting: Chart.js via vue-chartjs.
- Motion: GSAP counter animation in Act 1.

### Performance Behavior

- Acts 2-5 are lazy loaded using defineAsyncComponent.
- IntersectionObserver preloads sections before they enter view.
- The Act 1 counter animates only when visible.

### Styling and Theme

- All styles are centralized in src/style.css.
- The page background is solid black.
- Visual direction is Apple-inspired (SF Pro stack, clean cards, restrained accents).

### Accessibility

- Skip link to main story content.
- ARIA labels on story sections and major chart/visual blocks.
- Keyboard focus-visible styling.
- Reduced motion support via prefers-reduced-motion.

## Current Component Map

- src/App.vue: shell, skip link, story mount, scroll progress usage.
- src/views/QualityStory.vue: story sequencing, lazy loading, data wiring.
- src/components/ScrollProgress.vue: top scroll progress indicator.
- src/components/BarChart.vue: Act 2 expected vs actual chart.
- src/components/ActThreePattern.vue: defect type mini-bars, heatmap, root-cause cards.
- src/components/ActFourImpact.vue: cost, correlation, and customer impact panels.
- src/components/ActFiveSolution.vue: best practices, pilot outcomes, AR concept image, ROI calculator.

## Data Sources

All narrative values are sourced from local JSON files in src/data/:

- qualityOverview.json
- defectsByShift.json
- defectsTypes.json
- defectHeatmap.json
- inspectorStats.json
- costBreakdown.json
- correlations.json
- bestPractices.json
- pilotResults.json
- roicalculator.json

## Recent Updates Incorporated

- Removed obsolete AR mockup HTML files in favor of the image asset workflow.
- Consolidated all component-level CSS into a single src/style.css.
- Improved Act 2 chart readability:
  - wrapped x-axis labels
  - increased chart container height
  - tuned spacing and bar thickness
  - switched chart text (legend, axes, tooltips) to dark text on light surfaces
- Verified with successful production builds.

## Build and Run

```bash
npm install
npm run dev
npm run build
npm run preview
```

## Deployment

- Deployment target: Vercel.
- Build artifact: dist/.
- Vercel configuration: vercel.json.

## Known Boundaries

- Data is static JSON, not yet connected to live systems.
- Vuetify is installed but the current UI is primarily custom CSS and native HTML semantics.
- This brief describes the implemented state, not an aspirational backlog.

## Next Practical Enhancements

1. Add a lightweight test suite (component smoke tests + accessibility checks).
2. Add schema validation for src/data JSON files.
3. Add CI checks for npm run build and lint/type validation.

Last updated: May 1, 2026

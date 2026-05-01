# Satellite Quality Story

Interactive five-act data story about quality variance in satellite manufacturing, built with Vue 3 + TypeScript.

## Overview

The story walks through a single thread:

1. The scale of the defect problem.
2. The shift-based variance surprise.
3. Root causes behind the variance.
4. Business and customer impact.
5. Practical interventions and ROI.

Current UI direction is Apple-inspired with a solid black page background and light content cards.

## Current Stack

- Vue 3 (Composition API + script setup)
- TypeScript
- Vite 5
- Chart.js 4 + vue-chartjs 5
- GSAP (counter animation)

## Scripts

```bash
npm install
npm run dev
npm run build
npm run preview
```

## Current Project Structure

```text
src/
	App.vue
	main.ts
	style.css
	views/
		QualityStory.vue
	components/
		ScrollProgress.vue
		BarChart.vue
		ActThreePattern.vue
		ActFourImpact.vue
		ActFiveSolution.vue
	data/
		qualityOverview.json
		defectsByShift.json
		defectsTypes.json
		defectHeatmap.json
		inspectorStats.json
		costBreakdown.json
		correlations.json
		bestPractices.json
		pilotResults.json
		roicalculator.json

docs/
	BRIEF.md

public/
	vision-pro-inspector.png
```

## Implementation Notes

- All app styling is centralized in src/style.css and grouped by section comments.
- Acts 2-5 are lazy loaded in src/views/QualityStory.vue using defineAsyncComponent and IntersectionObserver.
- The Act 1 hero counter animates when it enters the viewport.
- Act 2 chart readability was tuned with wrapped labels, spacing, and dark chart text.
- Accessibility includes skip link, ARIA labels, keyboard focus styles, and reduced-motion handling.

## Testing and Validation

Primary validation step:

```bash
npm run build
```

Recent updates were validated with a successful production build.

## Deployment

- Build output is generated in dist/.
- Vercel config is available in vercel.json.

## License

MIT. See LICENSE.

Last updated: May 1, 2026

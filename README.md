# Satellite Quality Story - Interactive Data Narrative

> An interactive data story revealing how shift timing dramatically impacts defect rates in satellite component manufacturing.

## 🎯 Project Overview

This is "Seeing in the Dark" - an interactive narrative that uncovers a 3.2x higher defect rate on night shift production and explores actionable solutions grounded in data.

**Tech Stack:**
- Vue 3 with Composition API
- TypeScript
- Vite (build tool)
- Chart.js (visualizations)
- GSAP (animations)
- Vuetify 3 (UI components)

## 🚀 Quick Start

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build
```

## 📁 Project Structure

```
src/
├── components/          # Vue components
│   ├── ScrollProgress.vue
│   ├── AnimatedCounter.vue
│   ├── RevealChart.vue
│   ├── HeatMap.vue
│   ├── ROICalculator.vue
│   └── ...
├── views/               # Page-level components
│   └── QualityStory.vue
├── composables/         # Reusable logic
│   ├── useScrollAnimation.ts
│   └── useChartAnimation.ts
├── data/                # Mock data files (JSON)
│   ├── qualityOverview.json
│   ├── defectsByShift.json
│   └── ...
├── App.vue
├── main.ts
└── style.css

docs/
├── BRIEF.md             # Full project specification
├── design-decisions.md  # Design rationale
└── data-dictionary.md   # Data definitions

.claude/
├── context.md           # Project context for AI
└── memory-bank.md       # Key decisions and learnings
```

## 📖 The 5-Act Story

1. **Act 1: The Problem** — Establish stakes ($4.2M cost)
2. **Act 2: The Surprise** — Reveal shift-based variance
3. **Act 3: The Pattern** — Deep dive into root causes
4. **Act 4: The Impact** — Show full cost and consequences
5. **Act 5: The Solution** — Pilot results and ROI calculator

## 🎨 Design System

**Colors:**
- **Deep Blue** (#0D1B2A) — Main background
- **Bright Cyan** (#00D9FF) — Highlights & tech accents
- **Day Green** (#06D6A0) — Good quality
- **Night Red** (#E63946) — Critical issues
- **Purple** (#7209B7) — Future vision

**Typography:**
- Orbitron Bold — Story titles
- Roboto Condensed — Headings
- Roboto — Body text
- Roboto Mono — Data & metrics

## 🛠️ Development

**Key Components:**
- `ScrollProgress` — Fixed progress bar
- `AnimatedCounter` — Numbers counting up on scroll
- `RevealChart` — Charts that animate on viewport entry
- `HeatMap` — Custom heat map component
- `ROICalculator` — Interactive slider-based calculator
- `FutureVision` — AR visualization component

**Animations:**
- Scroll-triggered reveals using GSAP ScrollTrigger
- Chart animations on data update
- Counter animations on load
- Smooth transitions between states

## ♿ Accessibility

- WCAG 2.1 AA compliant
- Keyboard navigation throughout
- Screen reader support with ARIA labels
- Respects `prefers-reduced-motion`
- Color-blind friendly palettes
- Touch targets: 44px minimum

## 📊 Data Files

All data files are in `/src/data/`:
- `qualityOverview.json` — Overall metrics
- `defectsByShift.json` — Shift-based defect rates
- `defectTypes.json` — Defect category breakdown
- `defectHeatmap.json` — Hour-by-hour, day-by-day patterns
- `inspectorStats.json` — Staffing and experience data
- `costBreakdown.json` — Cost impact analysis
- `correlations.json` — Statistical relationships
- `pilotResults.json` — Before/after intervention data
- `roiCalculator.json` — ROI scenarios

## 🧪 Testing

Run the narrative flow test:
1. First-time viewer can follow story without confusion ✓
2. Each act builds on the previous one ✓
3. Insights are clearly stated, not buried ✓
4. Data feels realistic for aerospace manufacturing ✓
5. Interactive elements respond immediately ✓
6. Responsive design works on mobile/tablet ✓

## 🚢 Deployment

Deploy to Vercel with:
```bash
npm run build
# Deploy dist/ folder to Vercel
```

**Password Protection:**
Add to `vercel.json` for password-protected preview

## 📚 References

- Edward Tufte — Data visualization principles
- Stephen Few — Effective data displays
- Aerospace quality standards (AMS/AS)
- Manufacturing best practices
- Apple Vision Pro engagement context

## 📝 License

Licensed under MIT. See LICENSE file.

---

**Last Updated:** April 30, 2026  
**Version:** 1.0.0  
**Author:** [Your Name]

<template>
  <div class="quality-story">
    <!-- Act 1: The Problem -->
    <section class="story-act act-1" aria-label="Act 1: The Quality Problem - Introduction to the defect issue">
      <div class="act-content">
        <h1>The $4.2M Quality Problem</h1>
        <div class="hero-metrics">
          <article class="metric-card" role="region" aria-label="Defects metric">
            <div class="metric-value">
              <span class="counter" ref="counterRef" aria-live="polite">0</span>
            </div>
            <div class="metric-label">Defects Detected Last Year</div>
          </article>
          <article class="metric-card" role="region" aria-label="Cost impact metric">
            <div class="metric-value">$4.2M</div>
            <div class="metric-label">Total Cost Impact</div>
          </article>
        </div>
        <p class="story-text">In satellite manufacturing, a single defect can doom a $50M mission. Last year, we detected 2,847 defects.</p>
        <div class="scroll-indicator" aria-live="polite" aria-atomic="true">↓ Scroll to explore</div>
      </div>
    </section>

    <!-- Act 2: The Surprise -->
    <section class="story-act act-2" aria-label="Act 2: The Surprise - Unexpected defect variance analysis">
      <div class="act-content">
        <h2>It's Not What You Think</h2>
        <p class="story-text">We thought defects were random. The data told a different story. Actual defects exceeded expectations by 154%.</p>
        <BarChart :data="qualityData.expectedVsActual" />
      </div>
    </section>

    <!-- Act 3: The Pattern -->
    <section class="story-act act-3" aria-label="Act 3: The Pattern - Root cause analysis">
      <div class="act-content">
        <h2>The Root Causes</h2>
        <p class="story-text">Three key factors explain the variance:</p>
        <ActThreePattern
          :defect-types="defectTypesData"
          :heatmap="defectHeatmapData"
          :inspector-stats="inspectorStatsData"
        />
      </div>
    </section>

    <!-- Act 4: The Impact -->
    <section class="story-act act-4" aria-label="Act 4: The Impact - Ripple effects across supply chain">
      <div class="act-content">
        <h2>The Ripple Effect</h2>
        <p class="story-text">The costs compound across the supply chain:</p>
        <ActFourImpact :data="costBreakdownData" :correlations="correlationsData" />
      </div>
    </section>

    <!-- Act 5: The Solution -->
    <section class="story-act act-5" aria-label="Act 5: The Solution - Path forward and ROI projections">
      <div class="act-content">
        <h2>The Path Forward</h2>
        <p class="story-text">Data shows exactly what works:</p>
        <ActFiveSolution
          :best-practices="bestPracticesData"
          :pilot-data="pilotResultsData"
          :roi-config="roiCalculatorConfig"
        />
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'
import BarChart from '../components/BarChart.vue'
import ActThreePattern from '../components/ActThreePattern.vue'
import ActFourImpact from '../components/ActFourImpact.vue'
import ActFiveSolution from '../components/ActFiveSolution.vue'
import qualityData from '../data/qualityOverview.json'
import defectTypesData from '../data/defectsTypes.json'
import defectHeatmapData from '../data/defectHeatmap.json'
import inspectorStatsData from '../data/inspectorStats.json'
import costBreakdownData from '../data/costBreakdown.json'
import correlationsData from '../data/correlations.json'
import bestPracticesData from '../data/bestPractices.json'
import pilotResultsData from '../data/pilotResults.json'
import roiCalculatorConfig from '../data/roicalculator.json'

const counterRef = ref<HTMLElement | null>(null)

onMounted(() => {
  // Animate counter in Act 1
  if (counterRef.value) {
    gsap.to({ value: 0 }, {
      value: 2847,
      duration: 2,
      ease: 'power2.out',
      onUpdate: function() {
        if (counterRef.value) {
          counterRef.value.textContent = Math.round(this.targets()[0].value).toLocaleString()
        }
      }
    })
  }
})
</script>

<style scoped>
.quality-story {
  width: 100%;
}

.story-act {
  min-height: auto;
  display: flex;
  align-items: flex-start;
  justify-content: center;
  padding: var(--spacing-2xl) var(--spacing-xl);
  scroll-margin-top: 60px;
  position: relative;
  background: linear-gradient(180deg, rgba(20, 23, 29, 0.9), rgba(9, 10, 13, 0.98));
  border-top: 1px solid rgba(216, 163, 74, 0.08);
}

.story-act:nth-child(2n) {
  background: linear-gradient(180deg, rgba(15, 17, 21, 0.96), rgba(8, 9, 12, 1));
}

.act-content {
  width: 100%;
  max-width: 980px;
}

.act-1 {
  background:
    radial-gradient(circle at top center, rgba(216, 163, 74, 0.18), transparent 34%),
    linear-gradient(180deg, #17191e 0%, #0f1115 45%, #090a0d 100%);
  min-height: 100vh;
  align-items: center;
}

.hero-metrics {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: var(--spacing-xl);
  margin: var(--spacing-2xl) 0;
}

.metric-card {
  background: linear-gradient(180deg, rgba(22, 25, 31, 0.96), rgba(14, 16, 20, 0.98));
  border: 1px solid rgba(216, 163, 74, 0.18);
  border-radius: 16px;
  padding: var(--spacing-lg);
  text-align: center;
  box-shadow: 0 18px 40px rgba(0, 0, 0, 0.28);
  transition: transform 200ms ease, box-shadow 200ms ease;
}

.metric-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 18px 34px rgba(216, 163, 74, 0.16);
}

.metric-value {
  font-size: 2.5rem;
  font-weight: 700;
  color: var(--color-cyan);
  margin-bottom: var(--spacing-md);
}

.metric-label {
  font-size: 0.875rem;
  color: var(--color-text-secondary);
  text-transform: uppercase;
  letter-spacing: 0.16em;
}

.story-text {
  font-size: 1.25rem;
  color: var(--color-text-secondary);
  line-height: 1.8;
}

.counter {
  font-variant-numeric: tabular-nums;
}

.scroll-indicator {
  display: flex;
  justify-content: center;
  text-transform: uppercase;
  letter-spacing: 0.14em;
  font-size: 1.5rem;
  color: var(--color-cyan);
  margin-top: var(--spacing-2xl);
  animation: slideDown 1s cubic-bezier(0.16, 1, 0.3, 1) infinite;
}

@keyframes slideDown {
  0% { transform: translateY(-12px); opacity: 0.6; }
  100% { transform: translateY(4px); opacity: 1; }
}

.chart-container {
  background: linear-gradient(180deg, rgba(20, 23, 29, 0.96), rgba(11, 12, 15, 0.98));
  border: 1px solid rgba(216, 163, 74, 0.18);
  border-radius: 16px;
  padding: var(--spacing-3xl);
  margin: var(--spacing-2xl) 0;
  text-align: center;
  color: var(--color-text-muted);
  min-height: 400px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.placeholder {
  font-size: 1rem;
}

/* Responsive */
@media (max-width: 768px) {
  .story-act {
    min-height: auto;
    padding: var(--spacing-2xl) var(--spacing-md);
  }

  .hero-metrics {
    grid-template-columns: 1fr;
  }

  h1 {
    font-size: 2rem;
  }

  h2 {
    font-size: 1.5rem;
  }

  .story-text {
    font-size: 1rem;
  }
}
</style>

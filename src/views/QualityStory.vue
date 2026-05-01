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
    <section
      ref="act2Ref"
      class="story-act act-2"
      aria-label="Act 2: The Surprise - Unexpected defect variance analysis"
    >
      <div class="act-content">
        <h2>It's Not What You Think</h2>
        <p class="story-text">We thought defects were random. The data told a different story. Actual defects exceeded expectations by 154%.</p>
        <BarChart v-if="isAct2Loaded" :data="qualityData.expectedVsActual" />
        <div v-else class="chart-container" aria-live="polite">Preparing chart...</div>
      </div>
    </section>

    <!-- Act 3: The Pattern -->
    <section
      ref="act3Ref"
      class="story-act act-3"
      aria-label="Act 3: The Pattern - Root cause analysis"
    >
      <div class="act-content">
        <h2>The Root Causes</h2>
        <p class="story-text">Three key factors explain the variance:</p>
        <ActThreePattern
          v-if="isAct3Loaded"
          :defect-types="defectTypesData"
          :heatmap="defectHeatmapData"
          :inspector-stats="inspectorStatsData"
        />
        <div v-else class="chart-container" aria-live="polite">Loading root cause analysis...</div>
      </div>
    </section>

    <!-- Act 4: The Impact -->
    <section
      ref="act4Ref"
      class="story-act act-4"
      aria-label="Act 4: The Impact - Ripple effects across supply chain"
    >
      <div class="act-content">
        <h2>The Ripple Effect</h2>
        <p class="story-text">The costs compound across the supply chain:</p>
        <ActFourImpact v-if="isAct4Loaded" :data="costBreakdownData" :correlations="correlationsData" />
        <div v-else class="chart-container" aria-live="polite">Loading impact model...</div>
      </div>
    </section>

    <!-- Act 5: The Solution -->
    <section
      ref="act5Ref"
      class="story-act act-5"
      aria-label="Act 5: The Solution - Path forward and ROI projections"
    >
      <div class="act-content">
        <h2>The Path Forward</h2>
        <p class="story-text">Data shows exactly what works:</p>
        <ActFiveSolution
          v-if="isAct5Loaded"
          :best-practices="bestPracticesData"
          :pilot-data="pilotResultsData"
          :roi-config="roiCalculatorConfig"
        />
        <div v-else class="chart-container" aria-live="polite">Loading solution model...</div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { defineAsyncComponent, ref, onMounted, onUnmounted } from 'vue'
import { gsap } from 'gsap'
import qualityData from '../data/qualityOverview.json'
import defectTypesData from '../data/defectsTypes.json'
import defectHeatmapData from '../data/defectHeatmap.json'
import inspectorStatsData from '../data/inspectorStats.json'
import costBreakdownData from '../data/costBreakdown.json'
import correlationsData from '../data/correlations.json'
import bestPracticesData from '../data/bestPractices.json'
import pilotResultsData from '../data/pilotResults.json'
import roiCalculatorConfig from '../data/roicalculator.json'

const BarChart = defineAsyncComponent(() => import('../components/BarChart.vue'))
const ActThreePattern = defineAsyncComponent(() => import('../components/ActThreePattern.vue'))
const ActFourImpact = defineAsyncComponent(() => import('../components/ActFourImpact.vue'))
const ActFiveSolution = defineAsyncComponent(() => import('../components/ActFiveSolution.vue'))

const counterRef = ref<HTMLElement | null>(null)
const act2Ref = ref<HTMLElement | null>(null)
const act3Ref = ref<HTMLElement | null>(null)
const act4Ref = ref<HTMLElement | null>(null)
const act5Ref = ref<HTMLElement | null>(null)

const isAct2Loaded = ref(false)
const isAct3Loaded = ref(false)
const isAct4Loaded = ref(false)
const isAct5Loaded = ref(false)

let counterAnimated = false
let counterObserver: IntersectionObserver | null = null
let lazyObserver: IntersectionObserver | null = null

onMounted(() => {
  const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches

  // Use Intersection Observer to animate counter only when Act 1 scrolls into view.
  if (counterRef.value) {
    if (prefersReducedMotion) {
      counterRef.value.textContent = '2,847'
      counterAnimated = true
    }

    counterObserver = new IntersectionObserver(
      (entries) => {
        const entry = entries[0]

        if (entry.isIntersecting && !counterAnimated) {
          counterAnimated = true
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
          counterObserver?.unobserve(entry.target)
        }
      },
      { threshold: 0.5 }
    )

    if (!prefersReducedMotion) {
      counterObserver.observe(counterRef.value)
    }
  }

  if (!('IntersectionObserver' in window)) {
    isAct2Loaded.value = true
    isAct3Loaded.value = true
    isAct4Loaded.value = true
    isAct5Loaded.value = true
    return
  }

  // Load heavier acts before they enter the viewport.
  lazyObserver = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (!entry.isIntersecting) {
          return
        }

        if (entry.target === act2Ref.value) {
          isAct2Loaded.value = true
        } else if (entry.target === act3Ref.value) {
          isAct3Loaded.value = true
        } else if (entry.target === act4Ref.value) {
          isAct4Loaded.value = true
        } else if (entry.target === act5Ref.value) {
          isAct5Loaded.value = true
        }

        lazyObserver?.unobserve(entry.target)
      })
    },
    { rootMargin: '320px 0px', threshold: 0.05 }
  )

  ;[act2Ref.value, act3Ref.value, act4Ref.value, act5Ref.value].forEach((sectionRef) => {
    if (sectionRef) {
      lazyObserver?.observe(sectionRef)
    }
  })
})

onUnmounted(() => {
  counterObserver?.disconnect()
  lazyObserver?.disconnect()
  counterObserver = null
  lazyObserver = null
})
</script>

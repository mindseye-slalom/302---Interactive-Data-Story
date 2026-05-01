<template>
  <div class="act-three-layout">
    <article class="act-three-card" aria-label="Defect type pattern by shift">
      <h3>Defect Types by Shift</h3>
      <p class="card-subtitle">Visual defects dominate night shift and drive most of the quality gap.</p>

      <div class="type-list">
        <div v-for="item in defectTypes.categories" :key="item.category" class="type-row">
          <div class="type-header">
            <span class="type-name">{{ item.category }}</span>
            <span class="type-multiplier">{{ item.multiplier.toFixed(1) }}x vs day</span>
          </div>

          <div class="mini-bars" role="img" :aria-label="`${item.category} rates: day ${item.dayRate}%, swing ${item.swingRate}%, night ${item.nightRate}%`">
            <div class="mini-bar day" :style="{ width: `${scale(item.dayRate)}%` }">Day {{ item.dayRate }}%</div>
            <div class="mini-bar swing" :style="{ width: `${scale(item.swingRate)}%` }">Swing {{ item.swingRate }}%</div>
            <div class="mini-bar night" :style="{ width: `${scale(item.nightRate)}%` }">Night {{ item.nightRate }}%</div>
          </div>
        </div>
      </div>
    </article>

    <article class="act-three-card" aria-label="Defect heatmap by day and time block">
      <h3>Time-Based Defect Heatmap</h3>
      <p class="card-subtitle">The 2am-4am window is the danger zone, especially on weekends.</p>

      <div class="heatmap" role="img" aria-label="Heatmap showing hourly defect rates by day">
        <div class="heatmap-row header-row">
          <div class="corner-cell"></div>
          <div v-for="block in heatmap.timeBlocks" :key="block" class="header-cell">{{ block }}</div>
        </div>

        <div v-for="day in heatmap.days" :key="day.day" class="heatmap-row">
          <div class="day-label">{{ day.day }}</div>
          <div
            v-for="(value, index) in day.values"
            :key="`${day.day}-${index}`"
            class="heat-cell"
            :style="heatStyle(value)"
            :title="`${day.day} ${heatmap.timeBlocks[index]}: ${value}% defect rate`"
          >
            {{ value }}%
          </div>
        </div>
      </div>

      <p class="danger-note">Highest observed rate: {{ heatmap.peakWindow.rate }}% during {{ heatmap.peakWindow.window }}.</p>
    </article>

    <article class="act-three-card" aria-label="Root cause comparison between day and night shift">
      <h3>The Real Culprits</h3>
      <p class="card-subtitle">Night shift conditions, not people, explain most of the variance.</p>

      <div class="culprit-grid">
        <div class="culprit-item">
          <h4>Staffing</h4>
          <div class="compare-row">
            <span class="compare-label">Day</span>
            <span class="compare-value">{{ inspectorStats.staffing.day.inspectors }} inspectors / {{ inspectorStats.staffing.day.lines }} lines</span>
          </div>
          <div class="compare-row">
            <span class="compare-label">Night</span>
            <span class="compare-value">{{ inspectorStats.staffing.night.inspectors }} inspectors / {{ inspectorStats.staffing.night.lines }} lines</span>
          </div>
          <p class="impact-chip">Impact: {{ staffingImpact }}</p>
        </div>

        <div class="culprit-item">
          <h4>Experience</h4>
          <div class="compare-row">
            <span class="compare-label">Day</span>
            <span class="compare-value">{{ inspectorStats.experience.dayYears }} years avg</span>
          </div>
          <div class="compare-row">
            <span class="compare-label">Night</span>
            <span class="compare-value">{{ inspectorStats.experience.nightYears }} years avg</span>
          </div>
          <p class="impact-chip">Impact: {{ experienceImpact }}</p>
        </div>

        <div class="culprit-item">
          <h4>Lighting</h4>
          <div class="compare-row">
            <span class="compare-label">Day</span>
            <span class="compare-value">{{ inspectorStats.environment.dayLux }} lux</span>
          </div>
          <div class="compare-row">
            <span class="compare-label">Night</span>
            <span class="compare-value">{{ inspectorStats.environment.nightLux }} lux</span>
          </div>
          <p class="impact-chip">Impact: {{ lightingImpact }}</p>
        </div>

        <div class="culprit-item process-item">
          <h4>Process</h4>
          <div class="compare-row">
            <span class="compare-label">Day</span>
            <span class="compare-value">{{ inspectorStats.process.day }}</span>
          </div>
          <div class="compare-row">
            <span class="compare-label">Night</span>
            <span class="compare-value">{{ inspectorStats.process.night }}</span>
          </div>
          <p class="impact-chip">Impact: Night shift has fewer defect-catching checkpoints on critical components.</p>
        </div>
      </div>

      <p class="insight">{{ inspectorStats.insight }}</p>
    </article>
  </div>
</template>

<script setup lang="ts">
interface DefectTypeCategory {
  category: string
  dayRate: number
  swingRate: number
  nightRate: number
  multiplier: number
}

interface DefectTypesData {
  categories: DefectTypeCategory[]
}

interface HeatmapDay {
  day: string
  values: number[]
}

interface HeatmapData {
  timeBlocks: string[]
  peakWindow: {
    window: string
    rate: number
  }
  days: HeatmapDay[]
}

interface InspectorStatsData {
  staffing: {
    day: { inspectors: number; lines: number }
    night: { inspectors: number; lines: number }
  }
  experience: {
    dayYears: number
    nightYears: number
  }
  environment: {
    dayLux: number
    nightLux: number
  }
  process: {
    day: string
    night: string
  }
  insight: string
}

const props = defineProps<{
  defectTypes: DefectTypesData
  heatmap: HeatmapData
  inspectorStats: InspectorStatsData
}>()

const staffingDayCoverage = props.inspectorStats.staffing.day.inspectors / props.inspectorStats.staffing.day.lines
const staffingNightCoverage = props.inspectorStats.staffing.night.inspectors / props.inspectorStats.staffing.night.lines
const staffingDrop = Math.round((1 - (staffingNightCoverage / staffingDayCoverage)) * 100)

const experienceDrop = Math.round((1 - (props.inspectorStats.experience.nightYears / props.inspectorStats.experience.dayYears)) * 100)
const lightingDrop = Math.round((1 - (props.inspectorStats.environment.nightLux / props.inspectorStats.environment.dayLux)) * 100)

const staffingImpact = `${staffingDrop}% lower inspector coverage per line at night`
const experienceImpact = `${experienceDrop}% lower average inspection tenure at night`
const lightingImpact = `${lightingDrop}% lower inspection lighting at night`

const maxTypeRate = Math.max(...props.defectTypes.categories.flatMap((item) => [item.dayRate, item.swingRate, item.nightRate]))
const maxHeatValue = Math.max(...props.heatmap.days.flatMap((day) => day.values))

const scale = (value: number): number => (value / maxTypeRate) * 100

const heatStyle = (value: number): Record<string, string> => {
  const intensity = value / maxHeatValue
  return {
    backgroundColor: `rgba(255, 69, 58, ${0.2 + intensity * 0.75})`,
    borderColor: `rgba(255, 255, 255, ${0.08 + intensity * 0.2})`
  }
}
</script>
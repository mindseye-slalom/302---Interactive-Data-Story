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
          <p>Day: {{ inspectorStats.staffing.day.inspectors }} inspectors / {{ inspectorStats.staffing.day.lines }} lines</p>
          <p>Night: {{ inspectorStats.staffing.night.inspectors }} inspectors / {{ inspectorStats.staffing.night.lines }} lines</p>
        </div>

        <div class="culprit-item">
          <h4>Experience</h4>
          <p>Day avg: {{ inspectorStats.experience.dayYears }} years</p>
          <p>Night avg: {{ inspectorStats.experience.nightYears }} years</p>
        </div>

        <div class="culprit-item">
          <h4>Lighting</h4>
          <p>Day: {{ inspectorStats.environment.dayLux }} lux</p>
          <p>Night: {{ inspectorStats.environment.nightLux }} lux</p>
        </div>

        <div class="culprit-item process-item">
          <h4>Process</h4>
          <p>Day: {{ inspectorStats.process.day }}</p>
          <p>Night: {{ inspectorStats.process.night }}</p>
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

<style scoped>
.act-three-layout {
  display: grid;
  gap: var(--spacing-xl);
}

.act-three-card {
  background: var(--color-card-bg);
  border: 1px solid var(--color-border);
  border-radius: 12px;
  padding: var(--spacing-lg);
}

.card-subtitle {
  color: var(--color-text-secondary);
  margin-bottom: var(--spacing-md);
}

.type-list {
  display: grid;
  gap: var(--spacing-md);
}

.type-row {
  padding: var(--spacing-sm);
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-radius: 8px;
}

.type-header {
  display: flex;
  justify-content: space-between;
  gap: var(--spacing-sm);
  margin-bottom: var(--spacing-sm);
}

.type-name {
  font-weight: 700;
  color: var(--color-text-primary);
}

.type-multiplier {
  color: var(--color-night-red);
  font-weight: 700;
}

.mini-bars {
  display: grid;
  gap: 8px;
}

.mini-bar {
  min-height: 32px;
  border-radius: 6px;
  display: flex;
  align-items: center;
  padding: 0 10px;
  font-size: 0.95rem;
  font-weight: 600;
  color: #ffffff;
}

.mini-bar.day {
  background: linear-gradient(90deg, rgba(48, 209, 88, 0.9), rgba(48, 209, 88, 0.68));
}

.mini-bar.swing {
  background: linear-gradient(90deg, rgba(255, 214, 10, 0.9), rgba(255, 214, 10, 0.68));
}

.mini-bar.night {
  background: linear-gradient(90deg, rgba(255, 69, 58, 0.95), rgba(255, 69, 58, 0.75));
}

.heatmap {
  display: grid;
  gap: 8px;
}

.heatmap-row {
  display: grid;
  grid-template-columns: 110px repeat(6, minmax(0, 1fr));
  gap: 8px;
  align-items: center;
}

.header-cell,
.day-label,
.corner-cell {
  color: var(--color-text-secondary);
  font-size: 0.85rem;
}

.header-cell {
  text-align: center;
  font-weight: 600;
}

.day-label {
  font-weight: 700;
}

.heat-cell {
  min-height: 44px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 6px;
  border: 1px solid rgba(255, 255, 255, 0.12);
  font-size: 0.85rem;
  font-weight: 700;
  color: #ffffff;
}

.danger-note {
  margin-top: var(--spacing-sm);
  color: var(--color-night-red);
  font-weight: 700;
}

.culprit-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: var(--spacing-sm);
}

.culprit-item {
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 8px;
  padding: var(--spacing-sm);
}

.culprit-item h4 {
  color: var(--color-cyan);
  margin-bottom: 8px;
}

.culprit-item p {
  margin-bottom: 6px;
  font-size: 0.95rem;
  color: var(--color-text-primary);
}

.process-item {
  grid-column: 1 / -1;
}

.insight {
  margin-top: var(--spacing-md);
  font-size: 1.05rem;
  color: var(--color-cyan);
  font-weight: 700;
}

@media (max-width: 900px) {
  .heatmap-row {
    grid-template-columns: 90px repeat(6, minmax(0, 1fr));
    gap: 6px;
  }

  .heat-cell {
    min-height: 40px;
    font-size: 0.8rem;
  }
}

@media (max-width: 768px) {
  .culprit-grid {
    grid-template-columns: 1fr;
  }

  .process-item {
    grid-column: auto;
  }

  .heatmap {
    overflow-x: auto;
    padding-bottom: 8px;
  }

  .heatmap-row {
    min-width: 680px;
  }
}
</style>
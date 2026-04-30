<template>
  <div class="act-four-layout">
    <article class="impact-card" aria-label="Cost breakdown of quality defects">
      <h3>Cost Breakdown</h3>
      <p class="card-subtitle">Night shift defects cost 2.3x more because they are caught later in the process.</p>

      <div class="cost-bars" role="img" aria-label="Horizontal bars showing cost categories and percentages of total impact">
        <div v-for="item in data.categories" :key="item.label" class="cost-row">
          <div class="cost-header">
            <span class="label">{{ item.label }}</span>
            <span class="value">${{ (item.amount / 1000000).toFixed(1) }}M ({{ item.percent }}%)</span>
          </div>
          <div class="bar-track">
            <div class="bar-fill" :style="{ width: `${item.percent}%` }"></div>
          </div>
        </div>
      </div>
    </article>

    <article class="impact-card" aria-label="Correlation analysis between operational factors and defect rates">
      <h3>Correlation Analysis</h3>
      <p class="card-subtitle">Speed, experience, and complexity all strongly correlate with defect outcomes.</p>

      <div class="correlation-grid">
        <div class="correlation-panel">
          <h4>Production Speed vs Defect Rate</h4>
          <ul>
            <li v-for="point in correlations.speedVsDefects" :key="point.label">
              <span>{{ point.label }}</span>
              <span>{{ point.speedIndex }}% speed | {{ point.defectRate }}% defects</span>
            </li>
          </ul>
          <p class="correlation-insight">{{ correlations.insights.speed }}</p>
        </div>

        <div class="correlation-panel">
          <h4>Experience vs Defect Rate</h4>
          <ul>
            <li v-for="point in correlations.experienceVsDefects" :key="point.label">
              <span>{{ point.label }}</span>
              <span>{{ point.years }} years | {{ point.defectRate }}% defects</span>
            </li>
          </ul>
          <p class="correlation-insight">{{ correlations.insights.experience }}</p>
        </div>

        <div class="correlation-panel full-width">
          <h4>Part Complexity vs Defect Rate</h4>
          <ul>
            <li v-for="point in correlations.complexityVsDefects" :key="point.label">
              <span>{{ point.label }}</span>
              <span>{{ point.complexity }} complexity | {{ point.defectRate }}% defects</span>
            </li>
          </ul>
          <p class="correlation-insight">{{ correlations.insights.complexity }}</p>
        </div>
      </div>
    </article>

    <article class="impact-card" aria-label="Customer and schedule impact from defects">
      <h3>Customer Impact</h3>
      <p class="card-subtitle">Quality variation creates customer trust and schedule risk beyond direct manufacturing costs.</p>

      <div class="impact-metrics">
        <div class="metric">
          <span class="metric-label">Launch Delay</span>
          <span class="metric-value">{{ data.customerImpact.launchDelayMonths }} months</span>
        </div>
        <div class="metric">
          <span class="metric-label">Day Shift Satisfaction</span>
          <span class="metric-value">{{ data.customerImpact.daySatisfaction }}/100</span>
        </div>
        <div class="metric">
          <span class="metric-label">Night Shift Satisfaction</span>
          <span class="metric-value">{{ data.customerImpact.nightSatisfaction }}/100</span>
        </div>
        <div class="metric">
          <span class="metric-label">Repeat Defect Incidents</span>
          <span class="metric-value">{{ data.customerImpact.repeatIncidents }}</span>
        </div>
      </div>
    </article>
  </div>
</template>

<script setup lang="ts">
interface CostCategory {
  label: string
  amount: number
  percent: number
}

interface CostBreakdownData {
  totalCost: number
  categories: CostCategory[]
  customerImpact: {
    launchDelayMonths: number
    daySatisfaction: number
    nightSatisfaction: number
    repeatIncidents: number
  }
}

interface CorrelationPoint {
  label: string
  defectRate: number
}

interface CorrelationsData {
  speedVsDefects: Array<CorrelationPoint & { speedIndex: number }>
  experienceVsDefects: Array<CorrelationPoint & { years: number }>
  complexityVsDefects: Array<CorrelationPoint & { complexity: number }>
  insights: {
    speed: string
    experience: string
    complexity: string
  }
}

defineProps<{
  data: CostBreakdownData
  correlations: CorrelationsData
}>()
</script>

<style scoped>
.act-four-layout {
  display: grid;
  gap: var(--spacing-xl);
}

.impact-card {
  background: var(--color-card-bg);
  border: 1px solid var(--color-border);
  border-radius: 12px;
  padding: var(--spacing-lg);
}

.card-subtitle {
  color: var(--color-text-secondary);
  margin-bottom: var(--spacing-md);
}

.cost-bars {
  display: grid;
  gap: var(--spacing-sm);
}

.cost-row {
  display: grid;
  gap: 8px;
}

.cost-header {
  display: flex;
  justify-content: space-between;
  gap: var(--spacing-sm);
  font-size: 0.95rem;
}

.label {
  color: var(--color-text-primary);
  font-weight: 600;
}

.value {
  color: var(--color-cyan);
  font-weight: 700;
}

.bar-track {
  width: 100%;
  height: 14px;
  background: rgba(255, 255, 255, 0.08);
  border-radius: 999px;
  overflow: hidden;
}

.bar-fill {
  height: 100%;
  background: linear-gradient(90deg, rgba(255, 71, 87, 0.95), rgba(255, 183, 3, 0.9));
}

.correlation-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: var(--spacing-sm);
}

.correlation-panel {
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 8px;
  padding: var(--spacing-sm);
}

.correlation-panel h4 {
  color: var(--color-cyan);
  margin-bottom: 8px;
}

.correlation-panel ul {
  list-style: none;
  display: grid;
  gap: 6px;
  margin: 0;
  padding: 0;
}

.correlation-panel li {
  display: flex;
  justify-content: space-between;
  gap: var(--spacing-sm);
  font-size: 0.92rem;
  color: var(--color-text-primary);
}

.correlation-insight {
  margin-top: 10px;
  margin-bottom: 0;
  color: var(--color-text-secondary);
  font-size: 0.92rem;
}

.full-width {
  grid-column: 1 / -1;
}

.impact-metrics {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: var(--spacing-sm);
}

.metric {
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 8px;
  padding: var(--spacing-sm);
  display: grid;
  gap: 6px;
}

.metric-label {
  font-size: 0.85rem;
  color: var(--color-text-secondary);
}

.metric-value {
  font-size: 1.2rem;
  font-weight: 700;
  color: var(--color-cyan);
}

@media (max-width: 900px) {
  .impact-metrics {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}

@media (max-width: 768px) {
  .correlation-grid,
  .impact-metrics {
    grid-template-columns: 1fr;
  }

  .full-width {
    grid-column: auto;
  }
}
</style>
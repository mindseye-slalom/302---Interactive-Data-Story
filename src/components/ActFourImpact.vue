<template>
  <div class="act-four-layout">
    <article class="impact-card" aria-label="Cost breakdown of quality defects">
      <h3>Cost Breakdown</h3>
      <p class="card-subtitle">Night shift defects cost 2.3x more because they are caught later in the process.</p>

      <div class="cost-bars" role="img" aria-label="Horizontal bars showing cost categories and percentages of total impact">
        <div v-for="item in data.categories" :key="item.label" class="cost-row">
          <div class="cost-header">
            <span class="label">{{ item.label }}</span>
            <span class="cost-metrics">
              <span class="cost-chip">${{ (item.amount / 1000000).toFixed(1) }}M</span>
              <span class="cost-chip">{{ item.percent }}% of total</span>
            </span>
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
              <span class="corr-label">{{ point.label }}</span>
              <span class="corr-metrics">
                <span class="corr-chip">Speed: {{ point.speedIndex }}%</span>
                <span class="corr-chip">Defects: {{ point.defectRate }}%</span>
              </span>
            </li>
          </ul>
          <p class="correlation-insight">{{ correlations.insights.speed }}</p>
        </div>

        <div class="correlation-panel">
          <h4>Experience vs Defect Rate</h4>
          <ul>
            <li v-for="point in correlations.experienceVsDefects" :key="point.label">
              <span class="corr-label">{{ point.label }}</span>
              <span class="corr-metrics">
                <span class="corr-chip">Experience: {{ point.years }} years</span>
                <span class="corr-chip">Defects: {{ point.defectRate }}%</span>
              </span>
            </li>
          </ul>
          <p class="correlation-insight">{{ correlations.insights.experience }}</p>
        </div>

        <div class="correlation-panel full-width">
          <h4>Part Complexity vs Defect Rate</h4>
          <ul>
            <li v-for="point in correlations.complexityVsDefects" :key="point.label">
              <span class="corr-label">{{ point.label }}</span>
              <span class="corr-metrics">
                <span class="corr-chip">Complexity: {{ point.complexity }}</span>
                <span class="corr-chip">Defects: {{ point.defectRate }}%</span>
              </span>
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
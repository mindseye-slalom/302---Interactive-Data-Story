<template>
  <div class="act-five-layout">
    <!-- Section 5A: Best Practices -->
    <article class="solution-card" aria-label="Best practices from day shift operations">
      <h3>Best Practices from Day Shift</h3>
      <p class="card-subtitle">Day shift proves it's possible—we just need to replicate these conditions on night shift.</p>
      <div class="practices-grid">
        <div v-for="practice in bestPractices" :key="practice.id" class="practice-item">
          <h4>{{ practice.title }}</h4>
          <p>{{ practice.description }}</p>
          <span class="practice-highlight">{{ practice.detail }}</span>
        </div>
      </div>
    </article>

    <!-- Section 5B: Pilot Results -->
    <article class="solution-card" aria-label="Six-month pilot program results showing defect reduction">
      <h3>Pilot Program Results</h3>
      <p class="card-subtitle">6-month pilot on night shift: Combined interventions reduced defects by 67%.</p>

      <div class="pilot-results">
        <div class="result-row">
          <span class="intervention">Added 2 Inspectors</span>
          <div class="bar-mini">
            <div class="bar-fill" :style="{ width: '42%' }"></div>
          </div>
          <span class="impact">-42%</span>
        </div>

        <div class="result-row">
          <span class="intervention">Improved Lighting to 800 lux</span>
          <div class="bar-mini">
            <div class="bar-fill" :style="{ width: '28%' }"></div>
          </div>
          <span class="impact">-28%</span>
        </div>

        <div class="result-row">
          <span class="intervention">Peer Review on Critical Parts</span>
          <div class="bar-mini">
            <div class="bar-fill" :style="{ width: '35%' }"></div>
          </div>
          <span class="impact">-35%</span>
        </div>

        <div class="result-row">
          <span class="intervention">Slower Production Pace (10%)</span>
          <div class="bar-mini">
            <div class="bar-fill" :style="{ width: '31%' }"></div>
          </div>
          <span class="impact">-31%</span>
        </div>
      </div>

      <p class="pilot-insight">{{ pilotData.summary }}</p>
    </article>

    <!-- Section 5C: Future Vision (AR) -->
    <article class="solution-card ar-vision" aria-label="Future vision with augmented reality quality assistance">
      <h3>The Future of Quality Inspection</h3>
      <p class="card-subtitle">What if every inspector had superhuman vision?</p>

      <div class="ar-concept">
        <img
          src="/vision-pro-inspector.png"
          class="ar-visual"
          alt="Vision Pro inspector reviewing a payload module with augmented overlays showing pass and fail annotations, inspection results, part information, relevant specifications, and tool environment data."
        />

        <p class="ar-description">
          This concept image shows how augmented reality could transform quality inspection with in-context annotations, AI-assisted pass-fail guidance,
          and live reference data that helps inspectors resolve issues faster and more consistently.
        </p>
      </div>
    </article>

    <!-- Section 5D: ROI Calculator -->
    <article class="solution-card calculator-card" aria-label="Interactive ROI calculator for quality interventions">
      <h3>ROI Calculator</h3>
      <p class="card-subtitle">Explore different investment scenarios and see the financial impact.</p>

      <div class="calculator">
        <div class="calculator-controls">
          <div v-for="input in calculatorInputs" :key="input.id" class="control-group">
            <label :for="input.id">{{ input.label }}</label>

            <div v-if="input.type === 'boolean'" class="toggle-group">
              <input
                :id="input.id"
                v-model="calculatorState[input.id]"
                type="checkbox"
                :aria-label="input.label"
              />
              <span>{{ calculatorState[input.id] ? 'Enabled' : 'Disabled' }}</span>
            </div>

            <div v-else class="slider-group">
              <input
                :id="input.id"
                v-model.number="calculatorState[input.id]"
                type="range"
                :min="input.min"
                :max="input.max"
                :step="input.step"
                :aria-label="input.label"
              />
              <span class="value-display">{{ formatValue(input, calculatorState[input.id]) }}</span>
            </div>
          </div>
        </div>

        <div class="calculator-results">
          <div class="result-item">
            <span class="result-label">Annual Investment</span>
            <span class="result-value">${{ (calculatorResults.annualInvestment / 1000).toFixed(0) }}K</span>
          </div>

          <div class="result-item">
            <span class="result-label">Defect Reduction</span>
            <span class="result-value">{{ calculatorResults.defectReduction }}%</span>
          </div>

          <div class="result-item">
            <span class="result-label">Annual Savings</span>
            <span class="result-value">${{ (calculatorResults.annualSavings / 1000000).toFixed(2) }}M</span>
          </div>

          <div class="result-item highlight">
            <span class="result-label">Payback Period</span>
            <span class="result-value">{{ calculatorResults.paybackMonths }} months</span>
          </div>

          <div class="result-item highlight">
            <span class="result-label">5-Year ROI</span>
            <span class="result-value">{{ (calculatorResults.fiveYearROI * 100).toFixed(0) }}%</span>
          </div>
        </div>
      </div>
    </article>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, watch } from 'vue'

interface BestPractice {
  id: string
  title: string
  description: string
  detail: string
}

interface PilotData {
  summary: string
}

interface CalculatorInput {
  id: string
  label: string
  type?: string
  min?: number
  max?: number
  step?: number
  default: any
  costPerUnit?: number
  cost?: number
  costInitial?: number
  costAnnual?: number
  defectReductionPerUnit?: number
  defectReduction?: number
  defectReductionPer10k?: number
}

interface ROICalculatorConfig {
  inputs: CalculatorInput[]
  constants: {
    baselineDefects: number
    avgCostPerDefect: number
    currentAnnualCost: number
  }
}

const props = defineProps<{
  bestPractices: BestPractice[]
  pilotData: PilotData
  roiConfig: ROICalculatorConfig
}>()

// Initialize calculator state with defaults
const calculatorState = ref<Record<string, any>>({})

// Initialize state from config
watch(() => props.roiConfig, (newConfig) => {
  if (newConfig?.inputs) {
    const state: Record<string, any> = {}
    newConfig.inputs.forEach(input => {
      state[input.id] = input.default
    })
    calculatorState.value = state
  }
}, { immediate: true })

const calculatorInputs = computed(() => {
  return props.roiConfig?.inputs || []
})

const calculatorResults = computed(() => {
  const state = calculatorState.value
  const constants = props.roiConfig?.constants
  
  if (!state || !constants) {
    return {
      annualInvestment: 0,
      defectReduction: 0,
      annualSavings: 0,
      paybackMonths: 0,
      fiveYearROI: 0
    }
  }

  // Calculate total annual investment
  let annualInvestment = 0
  let totalDefectReduction = 0

  // Process staffing
  const staffingInput = calculatorInputs.value.find(i => i.id === 'staffing')
  if (staffingInput && state.staffing !== undefined) {
    const count = state.staffing
    annualInvestment += (count * (staffingInput.costPerUnit || 0))
    totalDefectReduction += (count * (staffingInput.defectReductionPerUnit || 0))
  }

  // Process lighting
  const lightingInput = calculatorInputs.value.find(i => i.id === 'lighting')
  if (lightingInput && state.lighting) {
    annualInvestment += (lightingInput.cost || 0)
    totalDefectReduction += (lightingInput.defectReduction || 0)
  }

  // Process training
  const trainingInput = calculatorInputs.value.find(i => i.id === 'training')
  if (trainingInput && state.training !== undefined) {
    annualInvestment += state.training
    const reduction = (state.training / 10000) * (trainingInput.defectReductionPer10k || 0)
    totalDefectReduction += reduction
  }

  // Process technology (AR)
  const techInput = calculatorInputs.value.find(i => i.id === 'technology')
  if (techInput && state.technology) {
    annualInvestment += (techInput.costInitial || 0) + (techInput.costAnnual || 0)
    totalDefectReduction += (techInput.defectReduction || 0)
  }

  // Cap defect reduction at 95%
  const defectReductionPercent = Math.min(totalDefectReduction, 95)
  
  // Calculate defects after reduction
  const defectsAfterReduction = constants.baselineDefects * (1 - defectReductionPercent / 100)
  const defectsSaved = constants.baselineDefects - defectsAfterReduction
  
  // Calculate annual savings
  const annualSavings = defectsSaved * constants.avgCostPerDefect
  
  // Calculate payback in months
  const paybackMonths = annualInvestment > 0 ? Math.ceil((annualInvestment / annualSavings) * 12) : 0
  
  // Calculate 5-year ROI: (Total savings over 5 years - Initial investment) / Initial investment
  const totalSavings = annualSavings * 5
  const fiveYearROI = annualInvestment > 0 ? (totalSavings - annualInvestment) / annualInvestment : 0

  return {
    annualInvestment,
    defectReduction: Math.round(defectReductionPercent),
    annualSavings,
    paybackMonths: Math.max(1, paybackMonths),
    fiveYearROI
  }
})

const formatValue = (input: CalculatorInput, value: any): string => {
  if (input.type === 'boolean') return value ? 'Yes' : 'No'
  if (input.id === 'training') return `$${value / 1000}K`
  if (input.id === 'staffing') return `${value} inspectors`
  return String(value)
}
</script>

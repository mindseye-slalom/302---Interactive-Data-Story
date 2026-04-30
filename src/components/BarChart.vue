<template>
  <div 
    class="bar-chart-wrapper"
    role="img"
    :aria-label="`Bar chart comparing expected vs actual defects across product lines. Total variance: ${86} (154%)`"
  >
    <p class="sr-only">Chart showing expected vs actual defects for each product line with variance calculations</p>
    <Bar
      :data="chartData"
      :options="chartOptions"
    />
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import { Bar } from 'vue-chartjs'
import {
  Chart as ChartJS,
  CategoryScale,
  LinearScale,
  BarElement,
  Title,
  Tooltip,
  Legend,
  ChartOptions
} from 'chart.js'

ChartJS.register(
  CategoryScale,
  LinearScale,
  BarElement,
  Title,
  Tooltip,
  Legend
)

interface ChartProps {
  data: Array<{
    product: string
    expected: number
    actual: number
    variance: number
  }>
}

const props = defineProps<ChartProps>()
const chartFontFamily = "'Segoe UI', -apple-system, BlinkMacSystemFont, 'SF Pro Display', sans-serif"

const chartData = computed(() => ({
  labels: props.data.map(d => d.product),
  datasets: [
    {
      label: 'Expected Defects',
      data: props.data.map(d => d.expected),
      backgroundColor: 'rgba(216, 163, 74, 0.62)',
      borderColor: 'rgba(216, 163, 74, 1)',
      borderWidth: 2,
      borderRadius: 6
    },
    {
      label: 'Actual Defects',
      data: props.data.map(d => d.actual),
      backgroundColor: 'rgba(255, 107, 87, 0.72)',
      borderColor: 'rgba(255, 107, 87, 1)',
      borderWidth: 2,
      borderRadius: 6
    }
  ]
}))

const chartOptions: ChartOptions<'bar'> = {
  responsive: true,
  maintainAspectRatio: false,
  font: {
    family: chartFontFamily
  },
  layout: {
    padding: {
      right: 0
    }
  },
  plugins: {
    legend: {
      display: true,
      position: 'top',
      labels: {
        color: 'rgba(255, 255, 255, 0.9)',
        font: {
          family: chartFontFamily,
          size: 13,
          weight: '600'
        },
        padding: 16,
        usePointStyle: true,
        pointStyle: 'circle'
      }
    },
    tooltip: {
      backgroundColor: 'rgba(17, 19, 24, 0.98)',
      titleColor: '#D8A34A',
      bodyColor: 'rgba(255, 255, 255, 0.9)',
      borderColor: '#D8A34A',
      borderWidth: 1,
      padding: 12,
      titleFont: {
        family: chartFontFamily,
        size: 13,
        weight: 'bold'
      },
      bodyFont: {
        family: chartFontFamily,
        size: 12
      },
      callbacks: {
        afterLabel: function(context) {
          if (context.datasetIndex === 1) {
            const dataIndex = context.dataIndex
            const variance = props.data[dataIndex].variance
            return `Variance: +${variance}`
          }
          return ''
        }
      }
    }
  },
  scales: {
    x: {
      offset: true,
      stacked: false,
      grid: {
        offset: true,
        color: 'rgba(255, 255, 255, 0.1)',
        drawBorder: false
      },
      ticks: {
        color: 'rgba(255, 255, 255, 0.7)',
        font: {
          family: chartFontFamily,
          size: 15,
          weight: '600'
        }
      }
    },
    y: {
      stacked: false,
      beginAtZero: true,
      grid: {
        color: 'rgba(255, 255, 255, 0.1)',
        drawBorder: false
      },
      ticks: {
        color: 'rgba(255, 255, 255, 0.7)',
        font: {
          family: chartFontFamily,
          size: 13,
          weight: '600'
        }
      }
    }
  }
}
</script>

<style scoped>
.bar-chart-wrapper {
  width: 100%;
  height: 360px;
  margin: 2rem 0;
  padding: 1.5rem;
  background: linear-gradient(180deg, rgba(20, 23, 29, 0.96), rgba(11, 12, 15, 0.98));
  border: 1px solid rgba(216, 163, 74, 0.2);
  border-radius: 16px;
  backdrop-filter: blur(8px);
}

/* Screen reader only content */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
</style>

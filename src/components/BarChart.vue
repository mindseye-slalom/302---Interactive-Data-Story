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
import { computed } from 'vue'
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

const wrappedLabels = computed(() =>
  props.data.map((d) => {
    const words = d.product.split(' ')
    if (words.length <= 2) {
      return words
    }
    const midpoint = Math.ceil(words.length / 2)
    return [words.slice(0, midpoint).join(' '), words.slice(midpoint).join(' ')]
  })
)

const chartData = computed(() => ({
  labels: wrappedLabels.value,
  datasets: [
    {
      label: 'Expected Defects',
      data: props.data.map(d => d.expected),
      backgroundColor: 'rgba(10, 132, 255, 0.62)',
      borderColor: 'rgba(100, 210, 255, 0.95)',
      borderWidth: 2,
      borderRadius: 6,
      maxBarThickness: 44
    },
    {
      label: 'Actual Defects',
      data: props.data.map(d => d.actual),
      backgroundColor: 'rgba(255, 69, 58, 0.72)',
      borderColor: 'rgba(255, 69, 58, 1)',
      borderWidth: 2,
      borderRadius: 6,
      maxBarThickness: 44
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
      left: 8,
      right: 8,
      bottom: 12
    }
  },
  plugins: {
    legend: {
      display: true,
      position: 'top',
      labels: {
        color: 'rgba(28, 28, 30, 0.92)',
        font: {
          family: chartFontFamily,
          size: 14,
          weight: 600
        },
        padding: 18,
        usePointStyle: true,
        pointStyle: 'circle'
      }
    },
    tooltip: {
      backgroundColor: 'rgba(255, 255, 255, 0.96)',
      titleColor: '#1d1d1f',
      bodyColor: 'rgba(29, 29, 31, 0.9)',
      borderColor: 'rgba(10, 132, 255, 0.45)',
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
        title: function(context) {
          const label = context[0]?.label
          return Array.isArray(label) ? label.join(' ') : String(label ?? '')
        },
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
        color: 'rgba(28, 28, 30, 0.14)'
      },
      ticks: {
        color: 'rgba(28, 28, 30, 0.82)',
        autoSkip: false,
        maxRotation: 0,
        minRotation: 0,
        padding: 8,
        font: {
          family: chartFontFamily,
          size: 12,
          weight: 600
        }
      }
    },
    y: {
      stacked: false,
      beginAtZero: true,
      grid: {
        color: 'rgba(28, 28, 30, 0.14)'
      },
      ticks: {
        color: 'rgba(28, 28, 30, 0.82)',
        callback: (value) => Number(value).toLocaleString(),
        font: {
          family: chartFontFamily,
          size: 13,
          weight: 600
        }
      }
    }
  }
}
</script>

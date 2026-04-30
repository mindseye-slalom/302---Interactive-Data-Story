<template>
  <div class="bar-chart-wrapper">
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

const chartData = computed(() => ({
  labels: props.data.map(d => d.product),
  datasets: [
    {
      label: 'Expected Defects',
      data: props.data.map(d => d.expected),
      backgroundColor: 'rgba(0, 217, 255, 0.6)',
      borderColor: 'rgba(0, 217, 255, 1)',
      borderWidth: 2,
      borderRadius: 6
    },
    {
      label: 'Actual Defects',
      data: props.data.map(d => d.actual),
      backgroundColor: 'rgba(255, 71, 87, 0.6)',
      borderColor: 'rgba(255, 71, 87, 1)',
      borderWidth: 2,
      borderRadius: 6
    }
  ]
}))

const chartOptions: ChartOptions<'bar'> = {
  responsive: true,
  maintainAspectRatio: true,
  plugins: {
    legend: {
      display: true,
      position: 'top',
      labels: {
        color: 'rgba(255, 255, 255, 0.9)',
        font: {
          family: "'Space Mono', monospace",
          size: 13,
          weight: '600'
        },
        padding: 16,
        usePointStyle: true,
        pointStyle: 'circle'
      }
    },
    tooltip: {
      backgroundColor: 'rgba(13, 27, 42, 0.95)',
      titleColor: '#00D9FF',
      bodyColor: 'rgba(255, 255, 255, 0.9)',
      borderColor: '#00D9FF',
      borderWidth: 1,
      padding: 12,
      titleFont: {
        size: 13,
        weight: 'bold'
      },
      bodyFont: {
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
      stacked: false,
      grid: {
        color: 'rgba(255, 255, 255, 0.1)',
        drawBorder: false
      },
      ticks: {
        color: 'rgba(255, 255, 255, 0.7)',
        font: {
          size: 11
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
          size: 11
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
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(0, 217, 255, 0.2);
  border-radius: 12px;
  backdrop-filter: blur(8px);
}
</style>

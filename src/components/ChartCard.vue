<template>
  <div class="chart-card">
    <h3>Clientes Nuevos (últimos meses)</h3>

    <!-- Gráfico de barras -->
    <div class="chart-container">
      <Bar :data="chartData" :options="chartOptions" />
    </div>

    <!-- Resumen interpretado -->
    <div class="summary">
      <p>📈 En octubre se registró un crecimiento del <strong>+25%</strong> respecto a septiembre.</p>
      <p>El número de clientes nuevos ha mostrado una tendencia constante al alza durante los últimos meses, reflejando una estrategia de captación efectiva.</p>
    </div>
  </div>
</template>

<script setup>
import { Bar } from 'vue-chartjs'
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale
} from 'chart.js'

// Registrar los componentes del gráfico
ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

// Datos del gráfico 📊 - COLORES LILAS CAMBIADOS
const chartData = {
  labels: ['Jun', 'Jul', 'Ago', 'Sep', 'Oct'],
  datasets: [
    {
      label: 'Clientes Nuevos',
      backgroundColor: [
        '#c4b5fd', // Lila más claro
        '#a78bfa', // Lila medio claro
        '#8b5cf6', // Lila medio
        '#7c3aed', // Lila medio oscuro
        '#6d28d9'  // Lila más oscuro
      ],
      borderRadius: 12,
      data: [25, 40, 32, 48, 60],
      hoverBackgroundColor: [
        '#ddd6fe',
        '#c4b5fd',
        '#a78bfa',
        '#8b5cf6',
        '#7c3aed'
      ]
    }
  ]
}

// Configuración del gráfico ⚙️
const chartOptions = {
  responsive: true,
  maintainAspectRatio: false,
  scales: {
    y: {
      beginAtZero: true,
      ticks: {
        color: '#6b7280',
        font: {
          size: 12,
          weight: '500'
        },
        stepSize: 10
      },
      grid: {
        color: '#f3f4f6',
        drawBorder: false
      }
    },
    x: {
      ticks: {
        color: '#6b7280',
        font: {
          size: 13,
          weight: '600'
        }
      },
      grid: {
        display: false
      }
    }
  },
  plugins: {
    legend: {
      display: false
    },
    tooltip: {
      backgroundColor: '#7c3aed',
      titleColor: '#fff',
      bodyColor: '#fff',
      padding: 12,
      cornerRadius: 8,
      displayColors: false,
      callbacks: {
        label: function(context) {
          return context.parsed.y + ' clientes'
        }
      }
    }
  }
}
</script>

<style scoped>
.chart-card {
  background-color: #ffffff;
  border-radius: 16px;
  padding: 1.5rem;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

h3 {
  text-align: center;
  color: #7c3aed;
  font-weight: 700;
  font-size: 1.125rem;
}

.chart-container {
  height: 300px;
}

.summary {
  background: linear-gradient(135deg, #faf5ff 0%, #f3e8ff 100%);
  border-radius: 12px;
  padding: 1rem 1.25rem;
  font-size: 0.95rem;
  color: #4b5563;
  line-height: 1.6;
  border-left: 4px solid #8b5cf6;
}

.summary p {
  margin: 0.5rem 0;
}

.summary strong {
  color: #7c3aed;
  font-weight: 700;
}
</style>
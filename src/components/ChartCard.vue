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

// Datos del gráfico 📊
const chartData = {
  labels: ['Jun', 'Jul', 'Ago', 'Sep', 'Oct'],
  datasets: [
    {
      label: 'Clientes Nuevos',
      backgroundColor: '#7b47f5',
      borderRadius: 12,
      data: [25, 40, 32, 48, 60] // Datos mensuales
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
        color: '#555',
        stepSize: 10
      },
      grid: {
        color: '#eee'
      }
    },
    x: {
      ticks: {
        color: '#555'
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
      backgroundColor: '#5a35f1',
      titleColor: '#fff',
      bodyColor: '#fff'
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
  color: #5a35f1;
  font-weight: 600;
}

.chart-container {
  height: 300px;
}

.summary {
  background-color: #f7f5ff;
  border-radius: 12px;
  padding: 1rem;
  font-size: 0.95rem;
  color: #333;
  line-height: 1.4;
}

.summary strong {
  color: #5a35f1;
}
</style>

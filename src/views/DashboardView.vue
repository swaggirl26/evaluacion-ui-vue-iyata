<template>
  <div class="dashboard">
    <Sidebar />
    <main class="content">
      <Header />

      <!-- Tarjetas superiores con íconos y tendencias -->
      <section class="cards">
        <Card 
          title="Ventas Totales"
          value="$12,500"
          :icon="DollarSign"
          color="purple"
          trend="up"
          :trend-value="12.5"
        />
        
        <Card 
          title="Clientes Activos"
          value="320"
          :icon="Users"
          color="purple"
          trend="up"
          :trend-value="8.2"
        />
        
        <Card 
          title="Nuevos Leads"
          value="45"
          :icon="TrendingUp"
          color="purple"
          trend="up"
          :trend-value="25"
        />
      </section>

      <!-- Gráficos lado a lado -->
      <section class="charts-row">
        <div class="chart-large">
          <ChartCard />
        </div>
        <div class="chart-small">
          <PieChart />
        </div>
      </section>
    </main>
  </div>
</template>

<script setup>
import Sidebar from '../components/Sidebar.vue'
import Header from '../components/Header.vue'
import Card from '../components/Card.vue'
import ChartCard from '../components/ChartCard.vue'
import PieChart from '../components/PieChart.vue'
import { DollarSign, Users, TrendingUp } from 'lucide-vue-next'
</script>

<style scoped>
.dashboard {
  display: flex;
  height: 100vh;
  background: linear-gradient(135deg, #f5f7fa 0%, #e8ecf1 100%);
}

.content {
  flex: 1;
  padding: 2rem;
  display: flex;
  flex-direction: column;
  overflow-y: auto;
}

.cards {
  display: flex;
  gap: 1.5rem;
  margin-bottom: 2rem;
  flex-wrap: wrap;
}

.charts-row {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 1.5rem;
  margin-bottom: 2rem;
}

.chart-large,
.chart-small {
  background-color: white;
  border-radius: 16px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
}

.chart-large {
  padding: 1.5rem;
}

@media (max-width: 1024px) {
  .charts-row {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 768px) {
  .dashboard {
    flex-direction: column;
  }

  .content {
    padding: 1rem;
  }

  .cards {
    flex-direction: column;
    gap: 1rem;
  }
}
</style>
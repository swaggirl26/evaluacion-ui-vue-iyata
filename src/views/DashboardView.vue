<template>
  <div class="dashboard">
    <Sidebar />
    <main class="content">
      <Header />

      <!-- Tarjetas superiores -->
      <section class="cards">
        <Card title="Ventas Totales" value="$12,500" />
        <Card title="Clientes Activos" value="320" />
        <Card title="Nuevos Leads" value="45" />
      </section>

      <!-- Gráfico resumen -->
      <section class="bottom-card">
        <ChartCard />
      </section>
    </main>
  </div>
</template>

<script setup>
import Sidebar from '../components/Sidebar.vue'
import Header from '../components/Header.vue'
import Card from '../components/Card.vue'
import ChartCard from '../components/ChartCard.vue'
</script>

<style scoped>
.dashboard {
  display: flex;
  height: 100vh;
}

.content {
  flex: 1;
  padding: 2rem;
  display: flex;
  flex-direction: column;
}

.cards {
  display: flex;
  gap: 1rem;
  margin-bottom: 1.5rem;
  flex-wrap: wrap;
}

/* Contenedor del gráfico */
.bottom-card {
  background-color: white;
  border-radius: 16px;
  padding: 1.5rem;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
  flex: 1;
}

/* Responsivo */
@media (max-width: 768px) {
  .dashboard {
    flex-direction: column;
  }

  .sidebar {
    width: 100%;
    height: auto;
    flex-direction: row;
  }

  .cards {
    flex-direction: column;
  }

  .bottom-card {
    padding: 1rem;
  }
}
</style>

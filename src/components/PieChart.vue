<template>
  <div class="pie-chart-container">
    <div class="chart-header">
      <h2 class="chart-title">Distribución de Ventas</h2>
      <div class="total-badge">
        <span class="total-label">Total</span>
        <span class="total-value">$45,200</span>
      </div>
    </div>

    <div class="chart-content">
      <div class="chart-wrapper">
        <svg viewBox="0 0 200 200" class="pie-chart">
          <!-- Círculo de fondo -->
          <circle
            cx="100"
            cy="100"
            r="80"
            fill="none"
            stroke="#f3f4f6"
            stroke-width="40"
          />
          
          <!-- Segmentos del gráfico -->
          <circle
            v-for="(segment, index) in segments"
            :key="index"
            cx="100"
            cy="100"
            r="80"
            :stroke="segment.color"
            :stroke-dasharray="`${segment.percentage * 5.027} 502.7`"
            :stroke-dashoffset="segment.offset"
            fill="transparent"
            stroke-width="40"
            class="pie-segment"
            :class="{ hovered: hoveredSegment === index }"
            @mouseenter="hoveredSegment = index"
            @mouseleave="hoveredSegment = null"
          />
          
          <!-- Centro -->
          <circle cx="100" cy="100" r="60" fill="white" />
         <text x="100" y="95" text-anchor="middle" class="center-percentage" transform="rotate(90 100 100)">
  {{ hoveredSegment !== null ? data[hoveredSegment].percentage : '100' }}%
</text>
<text x="100" y="112" text-anchor="middle" class="center-label" transform="rotate(90 100 100)">
  {{ hoveredSegment !== null ? data[hoveredSegment].label : 'Total' }}
</text>
        </svg>
      </div>

      <!-- Leyenda mejorada -->
      <div class="legend">
        <div 
          v-for="(item, index) in data" 
          :key="index"
          class="legend-item"
          :class="{ active: hoveredSegment === index }"
          @mouseenter="hoveredSegment = index"
          @mouseleave="hoveredSegment = null"
        >
          <div class="legend-info">
            <div class="legend-color-dot" :style="{ backgroundColor: item.color }"></div>
            <span class="legend-label">{{ item.label }}</span>
          </div>
          <div class="legend-stats">
            <span class="legend-percentage">{{ item.percentage }}%</span>
            <span class="legend-value">${{ formatValue(item.value) }}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const hoveredSegment = ref(null)

const data = ref([
  { label: 'Productos', percentage: 45, value: 20340, color: '#8b5cf6' },
  { label: 'Servicios', percentage: 30, value: 13560, color: '#a78bfa' },
  { label: 'Suscripciones', percentage: 15, value: 6780, color: '#c4b5fd' },
  { label: 'Otros', percentage: 10, value: 4520, color: '#e9d5ff' }
])

const segments = computed(() => {
  let currentOffset = 0
  return data.value.map(item => {
    const segment = {
      ...item,
      offset: -currentOffset
    }
    currentOffset += item.percentage * 5.027
    return segment
  })
})

const formatValue = (value) => {
  return (value / 1000).toFixed(1) + 'k'
}
</script>

<style scoped>
.pie-chart-container {
  background: white;
  border-radius: 16px;
  padding: 1.5rem;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
  height: 100%;
  display: flex;
  flex-direction: column;
}

.chart-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.5rem;
}

.chart-title {
  font-size: 1.25rem;
  font-weight: 700;
  color: #1f2937;
  margin: 0;
}

.total-badge {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  padding: 0.5rem 1rem;
  background: linear-gradient(135deg, #f3e8ff 0%, #e9d5ff 100%);
  border-radius: 12px;
}

.total-label {
  font-size: 0.75rem;
  color: #6b7280;
  font-weight: 500;
}

.total-value {
  font-size: 1.125rem;
  font-weight: 700;
  color: #7b47f5;
}

.chart-content {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  flex: 1;
}

.chart-wrapper {
  position: relative;
  width: 100%;
  max-width: 220px;
  margin: 0 auto;
}

.pie-chart {
  width: 100%;
  height: auto;
  transform: rotate(-90deg);
  filter: drop-shadow(0 4px 8px rgba(139, 92, 246, 0.1));
}

.pie-segment {
  transition: all 0.3s ease;
  cursor: pointer;
}

.pie-segment.hovered {
  stroke-width: 44;
  filter: brightness(1.1);
}

.center-percentage {
  font-size: 24px;
  fill: #1f2937;
  font-weight: 700;
}

.center-label {
  font-size: 11px;
  fill: #9ca3af;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.legend {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.legend-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.875rem 1rem;
  background: #f9fafb;
  border-radius: 12px;
  transition: all 0.2s;
  cursor: pointer;
  border: 2px solid transparent;
}

.legend-item:hover,
.legend-item.active {
  background: #f3f4f6;
  border-color: #e9d5ff;
  transform: translateX(4px);
}

.legend-info {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.legend-color-dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  flex-shrink: 0;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.legend-label {
  font-size: 0.875rem;
  color: #4b5563;
  font-weight: 600;
}

.legend-stats {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 0.125rem;
}

.legend-percentage {
  font-size: 0.875rem;
  color: #1f2937;
  font-weight: 700;
}

.legend-value {
  font-size: 0.75rem;
  color: #9ca3af;
  font-weight: 500;
}

@media (max-width: 768px) {
  .chart-wrapper {
    max-width: 180px;
  }
  
  .legend-item {
    padding: 0.75rem;
  }
}
</style>
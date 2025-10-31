<template>
  <div class="card" :style="{ backgroundColor: bgColor }">
    <div class="card-header">
      <div class="icon-container" v-if="icon" :style="{ background: iconBg }">
        <component :is="icon" :size="24" />
      </div>
      
      <div v-if="trend" class="trend-badge" :class="trendClass">
        <component :is="trendIcon" :size="14" />
        <span>{{ trendValue }}%</span>
      </div>
    </div>
    
    <h3>{{ title }}</h3>
    <p class="value">{{ value }}</p>
    
    <div v-if="showFooter" class="card-footer">
      <span>vs. mes anterior</span>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'
import { ArrowUp, ArrowDown } from 'lucide-vue-next'

const props = defineProps({
  title: {
    type: String,
    required: true
  },
  value: {
    type: [String, Number],
    required: true
  },
  icon: {
    type: Object,
    default: null
  },
  color: {
    type: String,
    default: 'purple'
  },
  trend: {
    type: String,
    default: null
  },
  trendValue: {
    type: Number,
    default: 0
  },
  showFooter: {
    type: Boolean,
    default: true
  }
})
const colorMap = {
  purple: { bg: '#7b47f5', icon: 'linear-gradient(135deg, #c084fc 0%, #a855f7 100%)' },
  slate: { bg: '#7b47f5', icon: 'linear-gradient(135deg, #e9d5ff 0%, #d8b4fe 100%)' },
  blue: { bg: '#7b47f5', icon: 'linear-gradient(135deg, #f3e8ff 0%, #e9d5ff 100%)' },
  green: { bg: '#7b47f5', icon: 'linear-gradient(135deg, #ddd6fe 0%, #c4b5fd 100%)' }
}
const bgColor = computed(() => colorMap[props.color]?.bg || colorMap.purple.bg)
const iconBg = computed(() => colorMap[props.color]?.icon || colorMap.purple.icon)
const trendIcon = computed(() => props.trend === 'up' ? ArrowUp : ArrowDown)
const trendClass = computed(() => ({
  'trend-positive': props.trend === 'up',
  'trend-negative': props.trend === 'down'
}))
</script>

<style scoped>
.card {
  color: white;
  padding: 1.5rem;
  border-radius: 16px;
  flex: 1;
  min-width: 250px;
  text-align: left;
  transition: all 0.3s ease;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  position: relative;
  overflow: hidden;
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 24px rgba(0, 0, 0, 0.15);
}

.card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(255,255,255,0.1) 0%, rgba(255,255,255,0) 100%);
  pointer-events: none;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 1.5rem;
  position: relative;
  z-index: 1;
}

.icon-container {
  width: 48px;
  height: 48px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  backdrop-filter: blur(10px);
}

.trend-badge {
  display: flex;
  align-items: center;
  gap: 4px;
  padding: 4px 8px;
  border-radius: 8px;
  font-size: 0.75rem;
  font-weight: 600;
  backdrop-filter: blur(10px);
}

.trend-positive {
  background-color: rgba(16, 185, 129, 0.2);
  color: #d1fae5;
}

.trend-negative {
  background-color: rgba(239, 68, 68, 0.2);
  color: #fecaca;
}

h3 {
  margin: 0 0 0.5rem 0;
  font-size: 0.875rem;
  font-weight: 500;
  opacity: 0.9;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.value {
  margin: 0;
  font-size: 2rem;
  font-weight: 700;
  line-height: 1;
}

.card-footer {
  margin-top: 1rem;
  padding-top: 1rem;
  border-top: 1px solid rgba(255, 255, 255, 0.2);
  font-size: 0.75rem;
  opacity: 0.8;
}

@media (max-width: 768px) {
  .card {
    min-width: 100%;
  }
  
  .value {
    font-size: 1.75rem;
  }
}
</style>
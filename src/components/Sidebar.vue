<template>
  <aside class="sidebar">
    <!-- Header con logo/avatar -->
    <div class="sidebar-header">
      <div class="logo">
        <div class="logo-icon">
          <LayoutDashboard :size="24" />
        </div>
        <span class="logo-text">Dashboard</span>
      </div>
    </div>

    <!-- Navegación principal -->
    <nav class="sidebar-nav">
      <a 
        v-for="item in menuItems" 
        :key="item.name"
        href="#"
        class="nav-item"
        :class="{ active: item.active }"
        @click.prevent="setActive(item.name)"
      >
        <component :is="item.icon" :size="20" />
        <span>{{ item.name }}</span>
      </a>
    </nav>

    <!-- Calendario mini integrado -->
    <div class="sidebar-calendar">
      <div class="calendar-header-mini">
        <h3>{{ currentMonthName }}</h3>
        <div class="calendar-nav-mini">
          <button @click="previousMonth" class="nav-btn-mini">
            <ChevronLeft :size="16" />
          </button>
          <button @click="nextMonth" class="nav-btn-mini">
            <ChevronRight :size="16" />
          </button>
        </div>
      </div>

      <div class="calendar-grid-mini">
        <div v-for="day in weekDaysShort" :key="day" class="day-header-mini">
          {{ day }}
        </div>
        <div
          v-for="(day, index) in calendarDays"
          :key="index"
          class="calendar-day-mini"
          :class="{
            'today': day.isToday,
            'other-month': day.isOtherMonth,
            'has-event': day.hasEvent
          }"
        >
          {{ day.number }}
        </div>
      </div>

      <!-- Próximo evento -->
      <div class="next-event">
        <div class="event-indicator" style="background: #7b47f5"></div>
        <div class="event-info">
          <p class="event-title">Reunión cliente</p>
          <p class="event-time">Hoy, 2:00 PM</p>
        </div>
      </div>
    </div>

    <!-- User info al final -->
    <div class="sidebar-footer">
      <div class="user-info">
        <div class="user-avatar">DG</div>
        <div class="user-details">
          <p class="user-name">Diana Gomez</p>
          <p class="user-role">Designer</p>
        </div>
      </div>
    </div>
  </aside>
</template>

<script setup>
import { ref, computed } from 'vue'
import { 
  LayoutDashboard, 
  Package, 
  Users, 
  Layers, 
  Inbox, 
  Settings,
  ChevronLeft,
  ChevronRight
} from 'lucide-vue-next'

const menuItems = ref([
  { name: 'Dashboard', icon: LayoutDashboard, active: true },
  { name: 'Products', icon: Package, active: false },
  { name: 'Customers', icon: Users, active: false },
  { name: 'Group', icon: Layers, active: false },
  { name: 'Inbox', icon: Inbox, active: false },
  { name: 'Settings', icon: Settings, active: false }
])

const setActive = (name) => {
  menuItems.value.forEach(item => {
    item.active = item.name === name
  })
}

// Calendario
const currentDate = ref(new Date())
const currentMonth = ref(currentDate.value.getMonth())
const currentYear = ref(currentDate.value.getFullYear())

const weekDaysShort = ['L', 'M', 'M', 'J', 'V', 'S', 'D']

const monthNames = [
  'Enero', 'Febrero', 'Marzo', 'Abril', 'Mayo', 'Junio',
  'Julio', 'Agosto', 'Septiembre', 'Octubre', 'Noviembre', 'Diciembre'
]

const currentMonthName = computed(() => monthNames[currentMonth.value])

const calendarDays = computed(() => {
  const firstDay = new Date(currentYear.value, currentMonth.value, 1)
  const lastDay = new Date(currentYear.value, currentMonth.value + 1, 0)
  const daysInMonth = lastDay.getDate()
  const startingDayOfWeek = firstDay.getDay() === 0 ? 6 : firstDay.getDay() - 1

  const days = []

  // Días del mes anterior
  const prevMonthLastDay = new Date(currentYear.value, currentMonth.value, 0).getDate()
  for (let i = startingDayOfWeek - 1; i >= 0; i--) {
    days.push({
      number: prevMonthLastDay - i,
      isOtherMonth: true,
      isToday: false,
      hasEvent: false
    })
  }

  // Días del mes actual
  const today = new Date()
  for (let i = 1; i <= daysInMonth; i++) {
    const isToday = 
      i === today.getDate() &&
      currentMonth.value === today.getMonth() &&
      currentYear.value === today.getFullYear()
    
    days.push({
      number: i,
      isOtherMonth: false,
      isToday,
      hasEvent: [30].includes(i)
    })
  }

  // Días del próximo mes
  const remainingDays = 35 - days.length
  for (let i = 1; i <= remainingDays; i++) {
    days.push({
      number: i,
      isOtherMonth: true,
      isToday: false,
      hasEvent: false
    })
  }

  return days
})

const previousMonth = () => {
  if (currentMonth.value === 0) {
    currentMonth.value = 11
    currentYear.value--
  } else {
    currentMonth.value--
  }
}

const nextMonth = () => {
  if (currentMonth.value === 11) {
    currentMonth.value = 0
    currentYear.value++
  } else {
    currentMonth.value++
  }
}
</script>

<style scoped>
.sidebar {
  width: 280px;
  background: white;
  border-right: 1px solid #e5e7eb;
  display: flex;
  flex-direction: column;
  height: 100vh;
  overflow-y: auto;
}

/* Header con logo */
.sidebar-header {
  padding: 1.5rem;
  border-bottom: 1px solid #f3f4f6;
}

.logo {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.logo-icon {
  width: 40px;
  height: 40px;
  background: linear-gradient(135deg, #7b47f5 0%, #6b3ee5 100%);
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
}

.logo-text {
  font-size: 1.25rem;
  font-weight: 700;
  color: #1f2937;
}

/* Navegación */
.sidebar-nav {
  padding: 1rem;
  flex: 1;
}

.nav-item {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.75rem 1rem;
  margin-bottom: 0.25rem;
  border-radius: 10px;
  color: #6b7280;
  text-decoration: none;
  font-size: 0.95rem;
  font-weight: 500;
  transition: all 0.2s;
  cursor: pointer;
}

.nav-item:hover {
  background: #f9fafb;
  color: #7b47f5;
}

.nav-item.active {
  background: linear-gradient(135deg, #7b47f5 0%, #6b3ee5 100%);
  color: white;
  box-shadow: 0 4px 12px rgba(123, 71, 245, 0.3);
}

.nav-item.active:hover {
  color: white;
}

/* Calendario mini */
.sidebar-calendar {
  padding: 1rem;
  border-top: 1px solid #f3f4f6;
  border-bottom: 1px solid #f3f4f6;
}

.calendar-header-mini {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.75rem;
}

.calendar-header-mini h3 {
  font-size: 0.875rem;
  font-weight: 700;
  color: #1f2937;
  margin: 0;
}

.calendar-nav-mini {
  display: flex;
  gap: 0.25rem;
}

.nav-btn-mini {
  width: 24px;
  height: 24px;
  background: #f3f4f6;
  border: none;
  border-radius: 6px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.2s;
  color: #6b7280;
}

.nav-btn-mini:hover {
  background: #e5e7eb;
  color: #374151;
}

.calendar-grid-mini {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 2px;
  margin-bottom: 0.75rem;
}

.day-header-mini {
  text-align: center;
  font-size: 0.625rem;
  font-weight: 600;
  color: #9ca3af;
  padding: 0.25rem 0;
}

.calendar-day-mini {
  aspect-ratio: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.625rem;
  border-radius: 6px;
  color: #374151;
  cursor: pointer;
  transition: all 0.2s;
}

.calendar-day-mini:hover {
  background: #f3f4f6;
}

.calendar-day-mini.other-month {
  color: #d1d5db;
}

.calendar-day-mini.today {
  background: #7b47f5;
  color: white;
  font-weight: 700;
}

.calendar-day-mini.has-event::after {
  content: '';
  position: absolute;
  bottom: 1px;
  width: 3px;
  height: 3px;
  background: #7b47f5;
  border-radius: 50%;
}

.calendar-day-mini.today.has-event::after {
  background: white;
}

.next-event {
  display: flex;
  gap: 0.5rem;
  padding: 0.75rem;
  background: #f9fafb;
  border-radius: 8px;
}

.event-indicator {
  width: 3px;
  border-radius: 2px;
  flex-shrink: 0;
}

.event-info {
  flex: 1;
}

.event-title {
  font-size: 0.75rem;
  font-weight: 600;
  color: #1f2937;
  margin: 0 0 0.125rem 0;
}

.event-time {
  font-size: 0.625rem;
  color: #6b7280;
  margin: 0;
}

/* Footer con usuario */
.sidebar-footer {
  padding: 1rem;
}

.user-info {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.75rem;
  background: #f9fafb;
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.2s;
}

.user-info:hover {
  background: #f3f4f6;
}

.user-avatar {
  width: 36px;
  height: 36px;
  background: linear-gradient(135deg, #7b47f5 0%, #6b3ee5 100%);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-weight: 700;
  font-size: 0.75rem;
  flex-shrink: 0;
}

.user-details {
  flex: 1;
}

.user-name {
  font-size: 0.875rem;
  font-weight: 600;
  color: #1f2937;
  margin: 0 0 0.125rem 0;
}

.user-role {
  font-size: 0.75rem;
  color: #6b7280;
  margin: 0;
}

@media (max-width: 768px) {
  .sidebar {
    width: 100%;
    height: auto;
  }
  
  .sidebar-calendar {
    display: none;
  }
}
</style>
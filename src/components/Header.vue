<template>
  <header class="header">
    <div class="search-container">
      <Search :size="20" class="search-icon" />
      <input 
        type="text" 
        placeholder="Buscar clientes, productos..." 
        class="search-input"
        v-model="searchQuery"
      />
      <button v-if="searchQuery" @click="clearSearch" class="clear-btn">
        <X :size="16" />
      </button>
    </div>

    <div class="header-actions">
      <button class="icon-btn" title="Notificaciones">
        <Bell :size="20" />
        <span class="notification-badge">3</span>
      </button>
      
      <button class="icon-btn" title="Mensajes">
        <MessageSquare :size="20" />
      </button>

      <button class="add-btn">
        <Plus :size="18" />
        <span>Nuevo</span>
      </button>
    </div>
  </header>
</template>

<script setup>
import { ref } from 'vue'
import { Search, Bell, MessageSquare, Plus, X } from 'lucide-vue-next'

const searchQuery = ref('')

const clearSearch = () => {
  searchQuery.value = ''
}
</script>

<style scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2rem;
  gap: 1.5rem;
}

/* Search Container */
.search-container {
  position: relative;
  flex: 1;
  max-width: 1000px;
}

.search-icon {
  position: absolute;
  left: 1rem;
  top: 50%;
  transform: translateY(-50%);
  color: #9ca3af;
  pointer-events: none;
}

.search-input {
  width: 100%;
  padding: 0.875rem 1rem 0.875rem 3rem;
  border: 2px solid #e5e7eb;
  border-radius: 12px;
  font-size: 0.95rem;
  background: white;
  transition: all 0.3s ease;
  color: #1f2937;
}

.search-input::placeholder {
  color: #9ca3af;
}

.search-input:focus {
  outline: none;
  border-color: #7b47f5;
  box-shadow: 0 0 0 4px rgba(123, 71, 245, 0.1);
}

.clear-btn {
  position: absolute;
  right: 0.75rem;
  top: 50%;
  transform: translateY(-50%);
  background: #f3f4f6;
  border: none;
  width: 24px;
  height: 24px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  color: #6b7280;
  transition: all 0.2s;
}

.clear-btn:hover {
  background: #e5e7eb;
  color: #374151;
}

/* Header Actions */
.header-actions {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.icon-btn {
  position: relative;
  width: 42px;
  height: 42px;
  background: white;
  border: 2px solid #e5e7eb;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  color: #6b7280;
  transition: all 0.2s;
}

.icon-btn:hover {
  background: #f9fafb;
  border-color: #7b47f5;
  color: #7b47f5;
}

.notification-badge {
  position: absolute;
  top: -4px;
  right: -4px;
  background: #ef4444;
  color: white;
  font-size: 0.625rem;
  font-weight: 700;
  padding: 2px 6px;
  border-radius: 9999px;
  min-width: 18px;
  text-align: center;
  border: 2px solid white;
}

.add-btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.25rem;
  background: linear-gradient(135deg, #7b47f5 0%, #6b3ee5 100%);
  color: white;
  border: none;
  border-radius: 12px;
  font-size: 0.95rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
  box-shadow: 0 4px 12px rgba(123, 71, 245, 0.3);
}

.add-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(123, 71, 245, 0.4);
}

.add-btn:active {
  transform: translateY(0);
}

@media (max-width: 768px) {
  .header {
    flex-direction: column;
    align-items: stretch;
  }

  .search-container {
    max-width: 100%;
  }

  .header-actions {
    justify-content: space-between;
  }

  .add-btn span {
    display: none;
  }

  .add-btn {
    width: 42px;
    padding: 0.75rem;
    justify-content: center;
  }
}
</style>
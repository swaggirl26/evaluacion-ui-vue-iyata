<template>
  <aside class="sidebar">
    <h2 class="logo">🟣 Dashboard</h2>
    <nav>
      <ul>
        <li v-for="item in menu" :key="item" :class="{ active: item === 'Dashboard' }">
          {{ item }}
        </li>
      </ul>
    </nav>
  </aside>
</template>

<script setup>
const menu = ["Dashboard", "Products", "Customers", "Group", "Inbox", "Settings", "Logout"]
</script>

<style scoped>
.sidebar {
  background-color: #f6f7fb;
  width: 220px;
  height: 100vh;
  padding: 2rem 1rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  border-right: 2px solid #e3e5ef;
}

.logo {
  font-weight: bold;
  color: #5a35f1;
  margin-bottom: 1rem;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

li {
  margin: 0.8rem 0;
  color: #707793;
  cursor: pointer;
  transition: color 0.2s;
}

li:hover,
.active {
  color: #5a35f1;
  font-weight: 600;
}
</style>

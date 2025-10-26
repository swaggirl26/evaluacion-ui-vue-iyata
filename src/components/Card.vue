<template>
  <div class="card">
    <h3>{{ title }}</h3>
    <p>{{ value }}</p>
  </div>
</template>

<script setup>
defineProps({
  title: String,
  value: String
})
</script>

<style scoped>
.card {
  background-color: var(--bg, #7b47f5);
  color: white;
  padding: 1.2rem;
  border-radius: 16px;
  flex: 1;
  min-width: 250px;
  text-align: center;
}
.card:nth-child(2) {
  background-color: #5a6378;
}
.card:nth-child(3) {
  background-color: #a98efb;
}
h3 {
  margin-bottom: 0.5rem;
}
</style>

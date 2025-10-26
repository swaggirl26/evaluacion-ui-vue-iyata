<template>
  <header class="header">
    <input type="text" placeholder="Search..." />
    <button>＋</button>
  </header>
</template>

<style scoped>
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #f2ecfb;
  padding: 0.75rem 1.5rem;
  border-radius: 16px;
  margin-bottom: 1.5rem;
}
input {
  flex: 1;
  padding: 0.6rem 1rem;
  border-radius: 10px;
  border: none;
  background-color: white;
  margin-right: 1rem;
  outline: none;
}
button {
  background-color: #7b47f5;
  color: white;
  border: none;
  font-size: 1.2rem;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  cursor: pointer;
}
button:hover {
  background-color: #6937d9;
}
</style>

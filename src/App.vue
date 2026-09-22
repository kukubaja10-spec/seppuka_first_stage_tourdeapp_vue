<script setup>
import { ref, onMounted } from 'vue'

const status = ref('Načítavam...')

onMounted(async () => {
  try {
    const response = await fetch('/api/v1/health')
    const data = await response.json()

    if (response.ok) {
      status.value = data.status.toUpperCase()
    } else {
      status.value = 'ERROR'
    }
  } catch (error) {
    status.value = 'ERROR'
  }
})
</script>

<template>
  <div class="app">
    <h1>Think different Academy</h1>
    <p>Status: {{ status }}</p>
  </div>
</template>

<style scoped>
.app {
  text-align: center;
  margin-top: 150px;
}

h1 {
  color: #000000;
  font-size: 60px;
}

p {
  font-size: 32px;
}
</style>
<script setup>
import { ref, watch } from 'vue'

const searchQuery = ref('')
const username = ref('')
const firstName = ref('')
const lastName = ref('')
const cart = ref([])

// Enkel watcher - nytt värde som parameter
watch(searchQuery, (newValue) => {
  console.log('Sökning ändrades till:', newValue)
  // Här skulle vi kunna göra API-anrop
})

// Watcher med både gammalt och nytt värde
watch(username, (newValue, oldValue) => {
  console.log(`Användarnamn: ${oldValue} → ${newValue}`)
})

// Watcher med options
watch(cart, (newCart) => {
  // Spara till localStorage när cart ändras
  localStorage.setItem('cart', JSON.stringify(newCart))
}, { deep: true }) // deep: true för att watcha nested properties

// Watcha flera källor samtidigt
watch([firstName, lastName], ([newFirst, newLast]) => {
  console.log(`Namn uppdaterat: ${newFirst} ${newLast}`)
})
</script>
<template>
  <div class="example-card">
    <h2>Watchers</h2>
    <input v-model="searchQuery" placeholder="Sök...">
    <input v-model="username" placeholder="Användarnamn">
  </div>
</template>

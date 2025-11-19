<script setup>
import { ref, computed } from 'vue'

// Reaktiv data
const firstName = ref('Anna')
const lastName = ref('Andersson')
const products = ref([
  { name: 'Bok', price: 100 },
  { name: 'Penna', price: 20 },
  { name: 'Sudd', price: 10 }
])
const searchQuery = ref('')

// Computed properties
const fullName = computed(() => {
  return `${firstName.value} ${lastName.value}`
})

const totalPrice = computed(() => {
  return products.value.reduce((sum, p) => sum + p.price, 0)
})

const filteredProducts = computed(() => {
  return products.value.filter(p => 
    p.name.toLowerCase().includes(searchQuery.value.toLowerCase())
  )
})
</script>
<template>
  <div class="example-card">
    <h2>Computed Properties</h2>
    <h2>Hej, {{ fullName }}!</h2>
    <p>Total: {{ totalPrice }} kr</p>
    
    <input v-model="searchQuery" placeholder="Sök produkt...">
    <ul>
      <li v-for="product in filteredProducts" :key="product.name">
        {{ product.name }} - {{ product.price }} kr
      </li>
    </ul>
  </div>
</template>

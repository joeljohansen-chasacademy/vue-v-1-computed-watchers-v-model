<!--
Övning: Produktlista med computed properties
Skapa en produktlista där användaren kan filtrera produkter och se statistik.

Uppgifter:
- Visa en lista med produkter (namn och pris)
- Sökfält för att filtrera produkter
- Visa endast produkter som matchar sökningen
- Visa totalpris för alla produkter
- Visa totalpris för filtrerade produkter
- Visa antal produkter som visas

Vad ni kommer behöva använda:
- ref() för produkter och söksträng
- computed() för filtrering och beräkningar
- v-model för sökfältet
- v-for för att lista produkter
-->

<script setup>
import { ref, computed } from 'vue'

const searchQuery = ref('')
const products = ref([
  { id: 1, name: 'Laptop', price: 8999 },
  { id: 2, name: 'Mus', price: 299 },
  { id: 3, name: 'Tangentbord', price: 599 },
  { id: 4, name: 'Skärm', price: 3499 },
  { id: 5, name: 'Högtalare', price: 799 }
])

// TODO: Skapa computed properties här
// Tips: Du behöver:
// - filteredProducts - Filtrera baserat på searchQuery
// - totalPrice - Summan av alla produkter
// - filteredTotal - Summan av filtrerade produkter
// - productCount - Antal filtrerade produkter

// computed() skapar en beräknad egenskap som automatiskt uppdateras
// när dess beroenden (searchQuery, products) ändras
const filteredProducts = computed(() => {
  // Filtrera produkter baserat på sökningen (case-insensitive)
  return products.value.filter(product => 
    product.name.toLowerCase().includes(searchQuery.value.toLowerCase())
  )
})

// Beräkna totalpris för alla produkter
const totalPrice = computed(() => {
  // reduce() summerar alla priser
  return products.value.reduce((sum, product) => sum + product.price, 0)
})

// Beräkna totalpris för endast filtrerade produkter
const filteredTotal = computed(() => {
  return filteredProducts.value.reduce((sum, product) => sum + product.price, 0)
})

// Räkna antal filtrerade produkter
const productCount = computed(() => {
  return filteredProducts.value.length
})

</script>

<template>
  <div>
    <h1>Produktkatalog</h1>
    
    <!-- TODO: Sökfält -->
    <div class="search">
      <!-- v-model skapar tvåvägsbindning mellan input och searchQuery -->
      <input v-model="searchQuery" placeholder="Sök produkt...">
    </div>

    <!-- TODO: Statistik -->
    <div class="stats">
      <p>Visar {{ productCount }} av {{ products.length }} produkter</p>
      <p>Totalt alla produkter: {{ totalPrice }} kr</p>
      <p>Totalt filtrerade: {{ filteredTotal }} kr</p>
    </div>

    <!-- TODO: Produktlista -->
    <ul class="product-list">
      <!-- v-for loopar igenom en array, :key behövs för Vue's rendering -->
      <li v-for="product in filteredProducts" :key="product.id">
        <span>{{ product.name }}</span>
        <span class="price">{{ product.price }} kr</span>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.search {
  margin: 1rem 0;
}

input {
  width: 100%;
  padding: 0.8rem;
  font-size: 1rem;
  border: 2px solid #ddd;
  border-radius: 4px;
  background: white;
  color: #333;
}

.stats {
  background: #f8f9fa;
  padding: 1rem;
  border-radius: 4px;
  margin: 1rem 0;
  color: #333; /* Mörk text för ljus bakgrund */
}

.product-list {
  list-style: none;
  padding: 0;
}

.product-list li {
  display: flex;
  justify-content: space-between;
  padding: 1rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  margin-bottom: 0.5rem;
  background: white;
  color: #333;
}

.price {
  font-weight: bold;
  color: #42b883;
}
</style>
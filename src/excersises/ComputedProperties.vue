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

</script>

<template>
  <div>
    <h1>Produktkatalog</h1>
    
    <!-- TODO: Sökfält -->
    <div class="search">
      <input placeholder="Sök produkt...">
    </div>

    <!-- TODO: Statistik -->
    <div class="stats">
      <p>Visar <!-- antal --> av {{ products.length }} produkter</p>
      <p>Totalt alla produkter: <!-- totalPrice --> kr</p>
      <p>Totalt filtrerade: <!-- filteredTotal --> kr</p>
    </div>

    <!-- TODO: Produktlista -->
    <ul class="product-list">
      <!-- Loopa igenom filteredProducts här -->
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
}

.stats {
  background: #f8f9fa;
  padding: 1rem;
  border-radius: 4px;
  margin: 1rem 0;
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
}

.price {
  font-weight: bold;
  color: #42b883;
}
</style>
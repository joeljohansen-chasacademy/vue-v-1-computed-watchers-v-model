<script setup>
import { ref, computed, watch } from 'vue'

// ===== REAKTIV DATA (från gårdagen (Lektion 1)) =====
const productName = ref('')
const productPrice = ref(0)
const budget = ref(500)
const searchQuery = ref('')
const products = ref([
  { id: 1, name: 'Mjölk', price: 15, bought: false },
  { id: 2, name: 'Bröd', price: 25, bought: false },
  { id: 3, name: 'Ost', price: 45, bought: false }
])

// ===== METODER Det vi gått igenom idag =====
const addProduct = () => {
  if (productName.value.trim() && productPrice.value > 0) {
    products.value.push({
      id: Date.now(),
      name: productName.value,
      price: Number(productPrice.value),
      bought: false
    })
    // Rensa formuläret
    productName.value = ''
    productPrice.value = 0
  }
}

const toggleBought = (id) => {
  const product = products.value.find(p => p.id === id)
  if (product) product.bought = !product.bought
}

const removeProduct = (id) => {
  products.value = products.value.filter(p => p.id !== id)
}

// ===== COMPUTED PROPERTIES Det vi gått igenom idag =====
// Filtrera produkter baserat på sökning
const filteredProducts = computed(() => {
  if (!searchQuery.value) return products.value
  return products.value.filter(p =>
    p.name.toLowerCase().includes(searchQuery.value.toLowerCase())
  )
})

// Totalpris för alla produkter
const totalPrice = computed(() => {
  return products.value.reduce((sum, p) => sum + p.price, 0)
})

// Totalpris för inköpta produkter
const spentAmount = computed(() => {
  return products.value
    .filter(p => p.bought)
    .reduce((sum, p) => sum + p.price, 0)
})

// Återstående budget
const remainingBudget = computed(() => {
  return budget.value - spentAmount.value
})

// Budgetstatus
const budgetStatus = computed(() => {
  if (remainingBudget.value < 0) return 'danger'
  if (remainingBudget.value < 100) return 'warning'
  return 'ok'
})

// ===== WATCHER (Lektion 2) =====
// Spara till localStorage när produkter ändras
watch(products, (newProducts) => {
  localStorage.setItem('shoppingList', JSON.stringify(newProducts))
  console.log('Shoppinglista sparad!')
}, { deep: true })

// Varna när budgeten är över
watch(remainingBudget, (newBudget) => {
  if (newBudget < 0) {
    alert('Du har överskridit din budget!')
  }
})

// Ladda sparad lista vid start
const savedList = localStorage.getItem('shoppingList')
if (savedList) {
  products.value = JSON.parse(savedList)
}
</script>

<template>
  <div class="shopping-list">
    <h1>Min Shoppinglista</h1>

    <!-- Budget-översikt -->
    <div class="budget-card" :class="budgetStatus">
      <h3>Budget: {{ budget }} kr</h3>
      <p>Spenderat: {{ spentAmount }} kr</p>
      <p>Kvar: {{ remainingBudget }} kr</p>
    </div>

    <!-- Lägg till produkt (v-model från Lektion 2) -->
    <div class="add-form">
      <h3>Lägg till produkt</h3>
      <input 
        v-model="productName" 
        placeholder="Produktnamn..."
        @keyup.enter="addProduct"
      >
      <input 
        v-model.number="productPrice" 
        type="number"
        placeholder="Pris..."
        @keyup.enter="addProduct"
      >
      <button @click="addProduct">Lägg till</button>
    </div>

    <!-- Sök/filtrera (v-model + computed) -->
    <div class="search">
      <input 
        v-model="searchQuery" 
        placeholder="🔍 Sök produkt..."
      >
      <p>Visar {{ filteredProducts.length }} av {{ products.length }} produkter</p>
    </div>

    <!-- Produktlista (v-for, v-if från Lektion 1) -->
    <div v-if="filteredProducts.length === 0" class="empty">
      <p>Inga produkter hittades</p>
    </div>
    
    <ul v-else class="product-list">
      <li 
        v-for="product in filteredProducts" 
        :key="product.id"
        :class="{ bought: product.bought }"
      >
        <input 
          type="checkbox"
          :checked="product.bought"
          @change="toggleBought(product.id)"
        >
        <span class="name">{{ product.name }}</span>
        <span class="price">{{ product.price }} kr</span>
        <button @click="removeProduct(product.id)" class="remove">🗑️</button>
      </li>
    </ul>

    <!-- Totalsumma (computed) -->
    <div class="total">
      <h3>Totalt i listan: {{ totalPrice }} kr</h3>
    </div>
  </div>
</template>

<style scoped>
.shopping-list {
  max-width: 600px;
  margin: 2rem auto;
  padding: 2rem;
  font-family: Arial, sans-serif;
}

.budget-card {
  padding: 1rem;
  border-radius: 8px;
  margin-bottom: 2rem;
}

.budget-card.ok { background: #223226; }
.budget-card.warning { background: #7a6008; }
.budget-card.danger { background: #61151b; }

.add-form, .search {
  margin-bottom: 1.5rem;
}

input {
  padding: 0.5rem;
  margin-right: 0.5rem;
  border: 1px solid #ddd;
  border-radius: 4px;
}

button {
  padding: 0.5rem 1rem;
  background: #42b883;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background: #35a372;
}

.product-list {
  list-style: none;
  padding: 0;
}

.product-list li {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  margin-bottom: 0.5rem;
}

.product-list li.bought {
  opacity: 0.6;
  text-decoration: line-through;
}

.name {
  flex: 1;
}

.price {
  font-weight: bold;
  color: #42b883;
}

.remove {
  background: #dc3545;
  padding: 0.25rem 0.5rem;
}

.total {
  margin-top: 2rem;
  padding-top: 1rem;
  border-top: 2px solid #42b883;
  text-align: right;
}

.empty {
  text-align: center;
  color: #999;
  padding: 2rem;
}
</style>
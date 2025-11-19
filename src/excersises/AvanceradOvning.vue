<!--
Övning: Varukorg med rabattkod
En mer avancerad övning som kombinerar v-model, computed properties och watchers.
Skapa en varukorg där användaren kan lägga till produkter, använda rabattkoder och 
automatiskt spara till localStorage.

Uppgifter:
- Input för produktnamn och pris
- Knapp för att lägga till produkter till varukorgen
- Lista som visar alla produkter i varukorgen
- Input för rabattkod
- Beräkna totalsumma, rabatt och slutpris
- Visa statistik om antal produkter och genomsnittspris
- Spara varukorgen till localStorage automatiskt
- Visa en statustext när varukorgen sparas
- Ladda sparad varukorg när sidan laddas

Rabattkoder som ska fungera:
- "SOMMER2024" - 15% rabatt
- "VIP" - 20% rabatt
- "STUDENT" - 10% rabatt

Vad ni kommer behöva använda:
- ref() för alla state-värden
- v-model för inputs
- computed() för:
  * Beräkna totalsumma
  * Beräkna rabattbelopp baserat på kod
  * Beräkna slutpris (totalsumma - rabatt)
  * Beräkna genomsnittspris
- watch() för att:
  * Spara varukorgen till localStorage
  * Visa statusmeddelande
- metoder för att:
  * Lägga till produkt
  * Ta bort produkt
-->

<script setup>
import { ref, computed, watch } from 'vue'

// State
const productName = ref('')
const productPrice = ref('')
const cart = ref([])
const discountCode = ref('')
const saveStatus = ref('')

// TODO: Ladda sparad varukorg från localStorage när komponenten laddas
// Tips: localStorage.getItem('cart') returnerar en sträng som behöver JSON.parse()

// TODO: Skapa metoder
// addProduct() - Lägg till produkt i cart
// Tips: 
// - Validera att båda fälten är ifyllda
// - Lägg till objekt med id, name och price
// - Rensa formulärfälten efteråt

// removeProduct(id) - Ta bort produkt från cart
// Tips: Använd filter() för att ta bort produkten med rätt id

// TODO: Skapa computed properties
// totalPrice - Summan av alla produktpriser i cart
// Tips: Använd reduce() för att summera

// discountPercent - Returnera rätt procentsats baserat på discountCode
// Tips: 
// - "SOMMER2024" = 15
// - "VIP" = 20
// - "STUDENT" = 10
// - Annat = 0

// discountAmount - Beräkna rabattbeloppet
// Tips: totalPrice * (discountPercent / 100)

// finalPrice - Slutpris efter rabatt
// Tips: totalPrice - discountAmount

// averagePrice - Genomsnittspris per produkt
// Tips: totalPrice / antal produkter (hantera division med 0)

// productCount - Antal produkter i varukorgen
// Tips: cart.value.length

// TODO: Watch för att spara varukorgen
// Tips:
// - Watcha 'cart' med { deep: true } för att fånga ändringar i arrayen
// - Spara till localStorage med localStorage.setItem('cart', JSON.stringify(cart.value))
// - Uppdatera saveStatus till "Varukorgen sparad!"
// - Använd setTimeout för att dölja meddelandet efter 2 sekunder

</script>

<template>
  <div>
    <h1>🛒 Min Varukorg</h1>
    
    <!-- TODO: Formulär för att lägga till produkt -->
    <div class="add-product">
      <h2>Lägg till produkt</h2>
      <div class="form-row">
        <input 
          type="text" 
          placeholder="Produktnamn"
        >
        <input 
          type="number" 
          placeholder="Pris"
        >
        <button>Lägg till</button>
      </div>
    </div>

    <!-- TODO: Rabattkod -->
    <div class="discount-section">
      <h3>Rabattkod</h3>
      <input 
        type="text" 
        placeholder="Ange rabattkod..."
      >
      <!-- Visa aktiv rabatt om det finns en -->
      <p v-if="discountPercent > 0" class="discount-active">
        ✓ Rabatt aktiv: {{ discountPercent }}%
      </p>
    </div>

    <!-- TODO: Varukorg -->
    <div class="cart">
      <h2>Varukorg (<!-- visa antal produkter -->)</h2>
      
      <!-- Visa meddelande om varukorgen är tom -->
      <p v-if="cart.length === 0" class="empty-cart">
        Din varukorg är tom. Lägg till produkter ovan!
      </p>

      <!-- TODO: Lista produkter -->
      <ul v-else class="cart-items">
        <!-- Loopa igenom cart här -->
        <!-- Visa produktnamn, pris och ta bort-knapp -->
      </ul>

      <!-- TODO: Sammanfattning -->
      <div v-if="cart.length > 0" class="summary">
        <div class="summary-row">
          <span>Antal produkter:</span>
          <span><!-- productCount --></span>
        </div>
        <div class="summary-row">
          <span>Genomsnittspris:</span>
          <span><!-- averagePrice --> kr</span>
        </div>
        <div class="summary-row">
          <span>Totalt:</span>
          <span><!-- totalPrice --> kr</span>
        </div>
        <div v-if="discountAmount > 0" class="summary-row discount">
          <span>Rabatt ({{ discountPercent }}%):</span>
          <span>-<!-- discountAmount --> kr</span>
        </div>
        <div class="summary-row total">
          <span><strong>Att betala:</strong></span>
          <span><strong><!-- finalPrice --> kr</strong></span>
        </div>
      </div>
    </div>

    <!-- Status -->
    <div class="save-status">
      {{ saveStatus }}
    </div>
  </div>
</template>

<style scoped>
.add-product {
  background: #f8f9fa;
  padding: 1.5rem;
  border-radius: 8px;
  margin-bottom: 2rem;
}

.add-product h2 {
  margin-top: 0;
}

.form-row {
  display: flex;
  gap: 1rem;
}

.form-row input {
  flex: 1;
  padding: 0.8rem;
  border: 2px solid #ddd;
  border-radius: 4px;
  font-size: 1rem;
}

.form-row button {
  padding: 0.8rem 2rem;
  background: #42b883;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
}

.form-row button:hover {
  background: #35a372;
}

.discount-section {
  background: #fff3cd;
  padding: 1rem;
  border-radius: 4px;
  margin-bottom: 2rem;
}

.discount-section h3 {
  margin-top: 0;
}

.discount-section input {
  width: 100%;
  padding: 0.8rem;
  border: 2px solid #ffc107;
  border-radius: 4px;
  font-size: 1rem;
  text-transform: uppercase;
}

.discount-active {
  color: #28a745;
  font-weight: bold;
  margin-top: 0.5rem;
}

.cart {
  background: white;
  padding: 1.5rem;
  border: 2px solid #ddd;
  border-radius: 8px;
}

.cart h2 {
  margin-top: 0;
}

.empty-cart {
  color: #999;
  font-style: italic;
  text-align: center;
  padding: 2rem;
}

.cart-items {
  list-style: none;
  padding: 0;
  margin: 0 0 1.5rem 0;
}

.cart-items li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  border-bottom: 1px solid #eee;
}

.cart-items li:last-child {
  border-bottom: none;
}

.remove-btn {
  background: #dc3545;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  cursor: pointer;
}

.remove-btn:hover {
  background: #c82333;
}

.summary {
  border-top: 2px solid #ddd;
  padding-top: 1rem;
}

.summary-row {
  display: flex;
  justify-content: space-between;
  padding: 0.5rem 0;
  font-size: 1rem;
}

.summary-row.discount {
  color: #28a745;
}

.summary-row.total {
  font-size: 1.3rem;
  border-top: 2px solid #333;
  margin-top: 0.5rem;
  padding-top: 1rem;
}

.save-status {
  text-align: center;
  margin-top: 1rem;
  color: #42b883;
  font-weight: bold;
  min-height: 1.5rem;
}
</style>


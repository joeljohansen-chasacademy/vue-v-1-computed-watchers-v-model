<!--
Övning: Räknare med metoder
Skapa en räknare där användaren kan utföra olika operationer med knappar.

Uppgifter:
- Visa ett tal som börjar på 0
- Knapp för att öka med 1
- Knapp för att minska med 1
- Knapp för att öka med 5
- Knapp för att dubbla värdet
- Knapp för att nollställa

Vad ni kommer behöva använda:
- ref() för att hålla räknarvärdet
- Metoder för varje operation
- @click för knappar
- {{ }} för att visa värdet
-->

<script setup>
import { ref } from 'vue'

const count = ref(0)

// TODO: Skapa metoder här
// Tips: Du behöver funktioner för att:
// - increment() - Öka med 1
// - decrement() - Minska med 1
// - addFive() - Öka med 5
// - double() - Dubbla värdet
// - reset() - Nollställ till 0

// Metoder för att manipulera räknaren
const increment = () => {
  count.value++ // .value behövs för att komma åt ref-värdet i script
}

const decrement = () => {
  count.value--
}

const addFive = () => {
  count.value += 5
}

const double = () => {
  count.value *= 2
}

const reset = () => {
  count.value = 0
}

</script>

<template>
  <div>
    <h1>Min Räknare</h1>
    
    <!-- TODO: Visa räknarvärdet -->
    <div class="display">
      <!-- I template behövs inte .value - Vue hanterar det automatiskt -->
      <h2>{{ count }}</h2>
    </div>

    <!-- TODO: Knappar för operationer -->
    <div class="buttons">
      <!-- @click är Vue's syntax för att lyssna på click-events -->
      <button @click="increment">+1</button>
      <button @click="decrement">-1</button>
      <button @click="addFive">+5</button>
      <button @click="double">×2</button>
      <button @click="reset">Nollställ</button>
    </div>
  </div>
</template>

<style scoped>
.display {
  font-size: 3rem;
  margin: 2rem 0;
  padding: 2rem;
  background: #f0f0f0;
  border-radius: 8px;
  color: #333; /* Mörk text för ljus bakgrund */
}

.buttons {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}

button {
  padding: 1rem 2rem;
  font-size: 1.2rem;
  border: none;
  border-radius: 4px;
  background: #42b883;
  color: white;
  cursor: pointer;
}

button:hover {
  background: #35a372;
}
</style>
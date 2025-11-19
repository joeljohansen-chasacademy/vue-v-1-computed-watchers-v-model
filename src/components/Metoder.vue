<script setup>
import { ref } from 'vue'

const count = ref(0)
const message = ref('')

// Metod 1: Arrow function (rekommenderat)
const increment = () => {
  count.value++
}

// Metod 2: Med parameter
const addNumber = (num) => {
  count.value += num
}

// Metod 3: Mer komplex logik
const resetAndNotify = () => {
  count.value = 0
  message.value = 'Räknaren är nollställd!'
  console.log('Reset utförd')
}
</script>   
<template>
  <div class="example-card">
    <h2>Metoder</h2>
    <h2>Räknare: {{ count }}</h2>
    <p>{{ message }}</p>
    
    <!-- Anropa metod utan parameter -->
    <button @click="increment">+1</button>
    
    <!-- Anropa metod MED parameter -->
    <button @click="addNumber(5)">+5</button>
    <button @click="addNumber(10)">+10</button>
    
    <!-- Anropa metod med flera operationer -->
    <button @click="resetAndNotify">Nollställ</button>
    
    <!-- Vi kan också anropa inline -->
    <button @click="count++">Inline +1</button>
  </div>
</template>



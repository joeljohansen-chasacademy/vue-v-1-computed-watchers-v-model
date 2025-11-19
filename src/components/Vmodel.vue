<script setup>
import { ref } from 'vue'

const name = ref('')
const message = ref('')
const newsletter = ref(false)
const age = ref(0) 
const bio = ref('')
</script>
<template>
  <div class="example-card">
    <h2>Vmodel</h2>
    <!-- Text input -->
    <input v-model="name" placeholder="Ditt namn">
    <p>Namn: {{ name }}</p>

    <!-- Textarea -->
    <textarea v-model="message" placeholder="Meddelande"></textarea>
    
    <!-- Checkbox (boolean) -->
    <input type="checkbox" v-model="newsletter" id="news">
    <label for="news">Prenumerera på nyhetsbrev</label>

<!-- .number - Konvertera automatiskt till nummer -->
    <input v-model.number="age" type="number">
    <p>Ålder + 10 = {{ age + 10 }}</p>
    
    <!-- .trim - Ta bort whitespace i början/slutet -->
    <input v-model.trim="bio">
    <p>Bio längd: {{ bio.length }}</p>
    <p>Namn: {{ name }}</p>
   
  </div>
</template>



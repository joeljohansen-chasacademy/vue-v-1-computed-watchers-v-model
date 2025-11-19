<!--
Övning: Användarformulär med v-model
Skapa ett formulär med olika typer av inputs och visa användarens val.

Uppgifter:
- Input för namn
- Textarea för bio
- Checkbox för godkänn villkor
- Select dropdown för favoritfärg
- Visa all inmatad data i en sammanfattning
- Knapp som är disabled tills användaren godkänt villkor

Vad ni kommer behöva använda:
- ref() för alla formulärfält
- v-model för alla inputs
- v-model.trim för namn
- :disabled för knappen
-->

<script setup>
import { ref } from 'vue'

const name = ref('')
const bio = ref('')
const acceptTerms = ref(false)
const favoriteColor = ref('')

// TODO: Lägg till en metod för att hantera formuläret
// const submitForm = () => { ... }

const submitForm = () => {
  // Här kan man göra något med formulärdata, t.ex. skicka till server
  console.log('Profil skapad:', {
    name: name.value,
    bio: bio.value,
    favoriteColor: favoriteColor.value
  })
}

</script>

<template>
  <div>
    <h1>Skapa profil</h1>
    
    <!--  använd @submit.prevent for att förhindra att sidan laddas om -->
    <form @submit.prevent="submitForm">
      <!-- TODO: Namn (text input med .trim) -->
      <div class="form-group">
        <label>Namn:</label>
        <!-- .trim tar automatiskt bort whitespace från början och slutet -->
        <input v-model.trim="name" type="text" placeholder="Ditt namn">
      </div>

      <!-- TODO: Bio (textarea med .trim) -->
      <div class="form-group">
        <label>Bio:</label>
        <textarea v-model.trim="bio" placeholder="Berätta om dig själv..." rows="4"></textarea>
      </div>
      <!-- TODO: Favoritfärg (select) -->
      <div class="form-group">
        <label>Favoritfärg:</label>
        <select v-model="favoriteColor">
          <option value="">Välj färg...</option>
          <option value="red">Röd</option>
          <option value="blue">Blå</option>
          <option value="green">Grön</option>
          <option value="yellow">Gul</option>
        </select>
      </div>

      <!-- TODO: Godkänn villkor (checkbox) -->
      <div class="form-group">
        <label>
          <!-- v-model med checkbox ger true/false -->
          <input v-model="acceptTerms" type="checkbox">
          Jag godkänner villkoren
        </label>
      </div>

      <!-- TODO: Submit-knapp (disabled om villkor ej godkända) -->
      <!-- :disabled binder disabled-attributet till ett boolean-värde -->
      <button type="submit" :disabled="!acceptTerms">Skapa profil</button>
    </form>

    <!-- TODO: Visa sammanfattning -->
    <div class="summary" v-if="name">
      <h2>Din profil:</h2>
      <p><strong>Namn:</strong> {{ name }}</p>
      <p><strong>Bio:</strong> {{ bio }}</p>
      <p><strong>Favoritfärg:</strong> {{ favoriteColor }}</p>
    </div>
  </div>
</template>

<style scoped>
.form-group {
  margin-bottom: 1.5rem;
}

label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: bold;
}

input[type="text"],
textarea,
select {
  width: 100%;
  padding: 0.5rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  background: white;
  color: #333;
}

.radio-group {
  display: flex;
  gap: 1rem;
}

button {
  padding: 0.8rem 2rem;
  background: #42b883;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
}

button:disabled {
  background: #ccc;
  cursor: not-allowed;
}

button:hover:not(:disabled) {
  background: #35a372;
}

.summary {
  margin-top: 2rem;
  padding: 1rem;
  background: #f8f9fa;
  border-radius: 4px;
  color: #333;
}
</style>
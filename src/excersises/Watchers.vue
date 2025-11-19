<!--
Övning: Anteckningsapp med watchers
Skapa en enkel anteckningsapp som automatiskt sparar till localStorage.

Uppgifter:
- Textarea där användaren kan skriva anteckningar
- Automatiskt spara till localStorage när texten ändras
- Visa en statustext när anteckningen sparas
- Visa antal tecken i anteckningen
- Ladda sparad anteckning när sidan laddas

Vad ni kommer behöva använda:
- ref() för anteckningen och statusmeddelande
- watch() för att reagera på ändringar
- v-model för textarea
- localStorage för att spara data
-->

<script setup>
import { ref, watch } from 'vue'

const note = ref('')
const saveStatus = ref('')
const charCount = ref(0)

// TODO: Ladda sparad anteckning från localStorage när komponenten laddas

// TODO: Watch för att spara till localStorage
// Tips: 
// - Watcha 'note'
// - Spara till localStorage med localStorage.setItem('note', note.value)
// - Uppdatera saveStatus till "Sparat!" 
// - Uppdatera charCount

// TODO: Watch för att dölja "Sparat!" efter 2 sekunder
// Tips: Använd setTimeout

</script>

<template>
  <div>
    <h1>📝 Mina Anteckningar</h1>
    
    <!-- TODO: Textarea för anteckning -->
    <textarea 
      placeholder="Skriv dina anteckningar här..."
      rows="10"
    ></textarea>

    <!-- TODO: Visa statistik -->
    <div class="info">
      <p>Antal tecken: <!-- charCount --></p>
      <p class="status">{{ saveStatus }}</p>
    </div>
  </div>
</template>

<style scoped>
textarea {
  width: 100%;
  padding: 1rem;
  font-size: 1rem;
  font-family: Arial, sans-serif;
  border: 2px solid #ddd;
  border-radius: 4px;
  resize: vertical;
}

.info {
  display: flex;
  justify-content: space-between;
  margin-top: 1rem;
  color: #666;
}

.status {
  color: #42b883;
  font-weight: bold;
}
</style>
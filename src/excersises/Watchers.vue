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
// Koden här körs när komponenten laddas (top-level i setup)
const savedNote = localStorage.getItem('note')
if (savedNote) {
  note.value = savedNote
  charCount.value = savedNote.length
}

// TODO: Watch för att spara till localStorage
// Tips: 
// - Watcha 'note'
// - Spara till localStorage med localStorage.setItem('note', note.value)
// - Uppdatera saveStatus till "Sparat!" 
// - Uppdatera charCount

// watch() lyssnar på ändringar och kör en funktion när värdet ändras
watch(note, (newValue) => {
  // Spara till localStorage
  localStorage.setItem('note', newValue)
  
  // Uppdatera antal tecken
  charCount.value = newValue.length
  
  // Visa sparmeddelande
  saveStatus.value = 'Sparat!'
  
  // Dölj meddelandet efter 2 sekunder
  setTimeout(() => {
    saveStatus.value = ''
  }, 2000)
})

// TODO: Watch för att dölja "Sparat!" efter 2 sekunder
// Tips: Använd setTimeout
// (Detta hanteras nu i samma watch ovan med setTimeout)

</script>

<template>
  <div>
    <h1>Min Anteckning</h1>
    
    <!-- TODO: Textarea för anteckning -->
    <textarea 
      v-model="note"
      placeholder="Skriv dina anteckningar här..."
      rows="10"
    ></textarea>

    <!-- TODO: Visa statistik -->
    <div class="info">
      <p>Antal tecken: {{ charCount }}</p>
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
  background: white;
  color: #333;
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
<script setup>
import Metoder from './components/Metoder.vue';
import ComputedProperties from './components/ComputedProperties.vue';
import Watchers from './components/Watchers.vue';
import VModel from './components/Vmodel.vue';
import Example from './components/ShoppingVagn.vue';
</script>

<template>
  <div id="app">
    <h1>Vue.js Metoder, computed & watch - Demo</h1>
<!-- 
    <Metoder />
    <ComputedProperties />
    <Watchers />
    <VModel /> -->
    <Example />
  </div>
</template>

<style scoped>
#app {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

h1 {
  text-align: center;
  margin-bottom: 30px;
}
</style>

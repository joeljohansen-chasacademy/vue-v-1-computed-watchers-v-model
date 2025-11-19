<script setup>
import Metoder from "./components/Metoder.vue";
import ComputedProperties from "./components/ComputedProperties.vue";
import Watchers from "./components/Watchers.vue";
import VModel from "./components/Vmodel.vue";
import ShoppingVagn from "./components/ShoppingVagn.vue";

import MetoderExcersise from "./excersises/Metoder.vue";
import ComputedPropertiesExcersise from "./excersises/ComputedProperties.vue";
import WatchersExcersise from "./excersises/Watchers.vue";
import VModelExcersise from "./excersises/Vmodel.vue";
import AvanceradOvning from "./excersises/AvanceradOvning.vue";
</script>

<template>
	<div id="app">
		<h1>Vue.js Metoder, computed & watch - Demo</h1>

		<h2>Exempel från lektionen</h2>
		<Metoder />
		<ComputedProperties />
		<Watchers />
		<VModel />
		<ShoppingVagn />
		<h2>Lösningar på övningarna</h2>
		<MetoderExcersise />
		<ComputedPropertiesExcersise />
		<WatchersExcersise />
		<VModelExcersise />
		<AvanceradOvning />
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

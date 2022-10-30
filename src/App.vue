<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Pokedex from "./components/Pokedex.vue";
</script>

<template>
  <div id="app">
    <Pokedex/>
  </div>
</template>

<style scoped>
body {
  margin: 0;
  padding: 0;
}
#app {
  background: radial-gradient(#1f1f1f, #151515);
}
</style>

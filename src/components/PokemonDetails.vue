<template>
  <div class="details">
    <div v-if="selectedPokemon.sprites">
      <img :src="selectedPokemon.sprites.front_default"/>
      <h3 class="pokemon-name">{{ selectedPokemon.name }}</h3>
      <p class="caracteristic"><span class="font-bold">Taille : </span>{{ selectedPokemon.height }} pouces</p>
      <p class="caracteristic"><span class="font-bold">Poids : </span>{{ selectedPokemon.weight }} ibs</p>
      <p class="caracteristic"><span class="font-bold">Types</span></p>
      <ul class="types">
        <li v-for="(type, index) in selectedPokemon.types">{{ type.type.name }}</li>
      </ul>
    </div>
    <div class="empty" v-else>
      <h3>Cliquez sur un Pokémon pour afficher ses détails.</h3>
    </div>
  </div>
</template>

<script>
export default {
  name: "PokemonDetails",
  props: [
    'selectedPokemon',
  ],
  updated() {
    console.log(this.selectedPokemon);
  }
}
</script>

<style scoped>
.details {
  display: flex;
  flex: 1;
  background-color: #fffaeb;
  border-radius: 24px;
  padding: 24px;
  margin-right: 24px;
}

h3 {
  font-weight: 600;
}

.pokemon-name {
  text-transform: capitalize;
}

.caracteristic {
  margin-top: 8px;
}

.font-bold {
  font-weight: 500;
}

.types {
  padding: 0;
}

.types li {
  margin-top: 8px;
  list-style: none;
  display: inline-block;
  margin-right: 4px;
  background-color: #e2e2e2;
  color: #181818;
  padding: 8px;
  border-radius: 16px;
  text-transform: uppercase;
}

.empty {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
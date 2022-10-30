<template>
  <div class="container">
    <img
        alt="Pokémon Logo"
        src="https://upload.wikimedia.org/wikipedia/commons/9/98/International_Pok%C3%A9mon_logo.svg"
    >
    <h1>Pokédex National</h1>
    <div class="pokedex">
      <PokemonsList :imageUrl="imageUrl" :apiUrl="apiUrl"/>
    </div>
  </div>
</template>

<script>
import PokemonsList from "./PokemonsList.vue";

export default {
  name: "Pokedex",
  data: () => {
    return {
      imageUrl:
          "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/",
      apiUrl: "https://pokeapi.co/api/v2/pokemon/",
      pokemon: "",
    };
  },
  components: {
    PokemonsList
  },
}
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
  width: calc(100% - 20px);
  min-height: calc(100vh - 20px);
  font-size: 1rem;
  font-weight: normal;
}

h1 {
  color: #fff;
  margin-top: 1rem;
}

.pokedex {
  display: flex;
  flex-wrap: wrap;
  margin-top: 24px;
  background: #e2e2e2;
  border-radius: 24px;
  padding: 24px 32px;
  width: 85%;
}
</style>
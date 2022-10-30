<template>
  <PokemonDetails :selected-pokemon="selectedPokemon" />

  <div class="list">
    Nombre de pokémons par page
    <select class="limit" v-model="limit" @change="handleSelectChange">
      <option>20</option>
      <option>50</option>
      <option>100</option>
    </select>
    <article v-for="(pokemon, index) in pokemons"
             :key="'poke'+index"
             @click="setPokemon(pokemon)">
      <img :src="imageUrl + pokemon.id + '.png'" width="48" height="48" alt="Pokémon Sprite">
      <h3>N°{{ pokemon.id }}</h3>
      <h3>{{ pokemon.name }}</h3>
    </article>
  </div>
</template>

<script>
import PokemonDetails from "./PokemonDetails.vue";
export default {
  name: "PokemonsList",
  components: {PokemonDetails},
  props: [
    'imageUrl',
    'apiUrl'
  ],
  data: () => {
    return {
      pokemons: [],
      nextUrl: '',
      currentUrl: '',
      selectedPokemon: {id: null, name: null},
      limit: 20
    }
  },
  methods: {
    fetchPokemonsList() {
      let req = new Request(this.currentUrl + '?limit=' + this.limit);
      fetch(req)
          .then((resp) => {
            if (resp.status === 200)
              return resp.json();
          })
          .then((data) => {
            this.nextUrl = data.next;
            data.results.forEach(pokemon => {
              pokemon.id = pokemon.url.split('/')
                  .filter(function (part) {
                    return !!part
                  }).pop();
              this.pokemons.push(pokemon);
            });
          })
          .catch((error) => {
            console.log(error);
          })
    },
    fetchPokemonDetails() {
      let req = new Request(this.selectedPokemon.url);
      fetch(req)
          .then((resp) => {
            if (resp.status === 200)
              return resp.json();
          })
          .then((data) => {
            this.selectedPokemon = {...data, name: this.selectedPokemon.name, id: this.selectedPokemon.id};
          })
          .catch((error) => {
            console.log(error);
          })
    },
    next() {
      this.currentUrl = this.nextUrl;
      this.fetchPokemonsList();
    },
    setPokemon(pokemon) {
      this.selectedPokemon = pokemon;
      this.fetchPokemonDetails();
    },
    handleSelectChange() {
      this.fetchPokemonsList();
    }
  },
  created() {
    this.currentUrl = this.apiUrl;
    this.fetchPokemonsList();
  },
}
</script>
<style scoped>
.list {
  display: inline-block;
  flex: 1;
  max-width: 510px;
  max-height: 600px;
  overflow-y: scroll;
}

article {
  display: flex;
  padding: 0 8px;
  margin-bottom: 4px;
  align-items: center;
  background-color: #fff1cc;
  text-align: center;
  text-transform: capitalize;
  border-radius: 24px;
  cursor: pointer;
}

h3 {
  margin: 0 8px;
}

.limit {
  margin-bottom: 8px;
}
</style>
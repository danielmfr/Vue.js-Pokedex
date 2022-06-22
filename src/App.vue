<template>
  <div id="bg-fixed"></div>
  <div class="column is-three-fifths is-offset-one-fifth">
    <figure class="image">
      <img src="./assets/pokedex_logo.png" />
    </figure>
  </div>

  <div class="column is-4 is-offset-4">
    <input
      type="text"
      class="input is-rounded"
      placeholder="Buscar Pokémon"
      v-model="busca"
      @keyup.enter="buscar"
    />
    <button class="button" id="buscaBtn" @click="buscar">Buscar</button>
  </div>

  <div class="columns is-multiline is-desktop mb-2 mx-5">
    <div
      v-for="pokemon in filteredPokemons"
      :key="pokemon.url"
      class="column is-one-third-desktop"
    >
      <Pokemon :name="pokemon.name" :url="pokemon.url" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon.vue";
export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: "",
    };
  },
  created() {
    axios
      //.get("https://pokeapi.co/api/v2/pokemon?limit=905&offset=0")
      .get("https://pokeapi.co/api/v2/pokemon?limit=100000&offset=0")
      .then((res) => {
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.results;
      });
  },
  methods: {
    buscar() {
      this.filteredPokemons = this.pokemons;
      if (this.busca == "" || this.busca == " ") {
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter(
          //(pokemon) => pokemon.name == this.busca
          (pokemon) => pokemon.name.includes(this.busca)
        );
      }
    },
  },
  computed: {
    /*resultadoBusca: function () {
      if (this.busca == "" || this.busca == " ") {
        return this.pokemons;
      } else {
        return this.pokemons.filter((pokemon) => pokemon.name == this.busca);
      }
    },*/
  },
  components: {
    Pokemon,
  },
};
</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
}
#bg-fixed {
  top: 0;
  left: 0;
  position: fixed;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background-image: linear-gradient(
    to top left,
    rgba(100, 100, 100, 1),
    rgba(162, 0, 0, 1)
  );
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#buscaBtn {
  margin-top: 2%;
}
</style>

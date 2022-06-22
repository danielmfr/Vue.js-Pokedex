<template>
  <div id="pokemon">
    <div class="card">
      <div class="card-image">
        <figure>
          <img :src="currentImg" />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{ pokemon.id }} - {{ upper }}</p>
            <Type :type1="pokemon.type1" :type2="pokemon.type2" />
          </div>
        </div>

        <div class="content">
          <button
            :class="{
              'button mr-2 selected': buttonSpriteSelected,
              'button mr-2': !buttonSpriteSelected,
            }"
            @click="flipSprite"
          >
            Virar sprite
          </button>
          <button
            :class="{
              'button selected': buttonShinySelected,
              button: !buttonShinySelected,
            }"
            @click="changeShiny"
          >
            Ver shiny
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Type from "./Type.vue";
export default {
  name: "CompPokemon",
  created() {
    axios.get(this.url).then((res) => {
      //console.log(res.data);
      if (res.data.types.length == 2) {
        this.pokemon.type1 = res.data.types[0].type.name;
        this.pokemon.type2 = res.data.types[1].type.name;
      } else {
        this.pokemon.type1 = res.data.types[0].type.name;
      }
      /*axios.get(res.data.types[0].type.url).then((res) => {
              console.log(res.data);
            });*/
      this.pokemon.id = res.data.id;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      this.pokemon.frontShiny = res.data.sprites.front_shiny;
      this.pokemon.backShiny = res.data.sprites.back_shiny;
      this.currentImg = this.pokemon.front;
    });
  },
  data() {
    return {
      pokemon: {
        id: 0,
        type1: "",
        type2: "",
        front: "",
        back: "",
        frontShiny: "",
        backShiny: "",
      },
      isFront: true,
      isShiny: false,
      currentImg: "",
      buttonSpriteSelected: false,
      buttonShinySelected: false,
    };
  },
  props: {
    name: String,
    url: String,
  },
  methods: {
    flipSprite() {
      this.buttonSpriteSelected = !this.buttonSpriteSelected;
      if (this.isFront) {
        this.isFront = false;
        this.isShiny
          ? (this.currentImg = this.pokemon.backShiny)
          : (this.currentImg = this.pokemon.back);
      } else {
        this.isFront = true;
        this.isShiny
          ? (this.currentImg = this.pokemon.frontShiny)
          : (this.currentImg = this.pokemon.front);
      }
    },
    changeShiny() {
      this.buttonShinySelected = !this.buttonShinySelected;
      if (!this.isShiny) {
        this.isShiny = true;
        this.isFront
          ? (this.currentImg = this.pokemon.frontShiny)
          : (this.currentImg = this.pokemon.backShiny);
      } else {
        this.isShiny = false;
        this.isFront
          ? (this.currentImg = this.pokemon.front)
          : (this.currentImg = this.pokemon.back);
      }
    },
  },
  computed: {
    upper() {
      var newName = this.name[0].toUpperCase() + this.name.slice(1);
      return newName;
    },
  },
  components: { Type },
};
</script>

<style>
.button {
  border-color: #535353 !important;
  box-shadow: none !important;
}
.selected {
  border-color: transparent !important;
  color: #fff !important;
  background-color: #3d3d3d !important;
  box-shadow: none !important;
}
</style>
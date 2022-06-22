<template>
  <div class="is-flex is-justify-content-center">
    <div :class="'mr-2 type ' + type1">
      {{ upperCaseType1 }}
    </div>
    <div v-if="type2" :class="'type ' + type2">
      {{ upperCaseType2 }}
    </div>
  </div>
</template>

<script>
export default {
  name: "CompType",
  props: {
    type1: String,
    type2: String,
  },
  computed: {
    upperCaseType1() {
      return this.type1.toUpperCase();
    },
    upperCaseType2() {
      return this.type2.toUpperCase();
    },
  },
};
</script>

<style>
.type {
  width: 100px !important;
  border: 1px solid !important;
  border-radius: 2em !important;
}
.type.grass {
  border-color: green !important;
  color: green !important;
}
.type.fire {
  border-color: red !important;
  color: red !important;
}
.type.water {
  border-color: blue !important;
  color: blue !important;
}
.type.poison {
  border-color: purple !important;
  color: purple !important;
}
.type.electric {
  border-color: #f8d539 !important;
  color: #f8d539 !important;
}
.type.bug {
  border-color: yellowgreen !important;
  color: yellowgreen !important;
}
.type.normal {
  border-color: gray !important;
  color: gray !important;
}
.type.flying {
  border-color: lightblue !important;
  color: lightblue !important;
}
.type.ice {
  border-color: rgb(0, 230, 230) !important;
  color: rgb(0, 230, 230) !important;
}
.type.dragon {
  border-color: #7038f8 !important;
  color: #7038f8 !important;
}
.type.rock {
  border-color: darkgoldenrod !important;
  color: darkgoldenrod !important;
}
.type.ground {
  border-color: burlywood !important;
  color: burlywood !important;
}
.type.fairy {
  border-color: pink !important;
  color: pink !important;
}
.type.steel {
  border-color: darkslategray !important;
  color: darkslategray !important;
}
.type.psychic {
  border-color: #e25e83 !important;
  color: #e25e83 !important;
}
.type.fighting {
  border-color: #c03028 !important;
  color: #c03028 !important;
}
.type.ghost {
  border-color: #725a9c !important;
  color: #725a9c !important;
}
.type.dark {
  border-color: #705848 !important;
  color: #705848 !important;
}
</style>
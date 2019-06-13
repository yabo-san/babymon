<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="babymon"/>
    <card :url="element.pokemon.url" v-for="(element, index) in pokemonOfRockType.pokemon" :key="index"></card>
    <div>

    </div>
    <div v-for="(element, index) in pokemonOfRockType.pokemon" :key="index">
      {{element.pokemon.url}}
    </div>

  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import card from "./components/card.vue";

export default {
  name: "app",
  components: {
    HelloWorld,
    card
  },
  data: function() {
    return { pokemonOfRockType: "" };
  },
  mounted: function() {
    const axios = require("axios");
    const vm = this;
    axios({
      method: "get",
      url: "http://pokeapi.co/api/v2/type/rock"
    }).then(function(response) {
      console.log(response.data.pokemon);
      vm.pokemonOfRockType = response.data;
    });
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

<template>
  <div id="app">
    <div class="container">
      <h1 class="text-center display-1">rock on \m/</h1>
      <div class="row">
        <card
          :url="element.pokemon.url"
          v-for="(element, index) in pokemonOfRockType.pokemon"
          :key="index"
          style= "margin-bottom: 30px"
        ></card>
      </div>
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


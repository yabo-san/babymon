
<template>
  <div id="app">
    <div class="container">
      <h1 class="text-center display-1">
        <span class="text-capitalize">{{activeType}}</span> on \m/
      </h1>
      <span
        v-for="type in types"
        :key="type.name"
        class="btn btn-primary m-1"
        v-on:click="somethingHappened(type.name)"
      >{{ type.name }}</span>
      <div class="row">
        <card
          :url="item.pokemon.url"
          v-for="item in pokemonOfCurrentType"
          :key="item.pokemon.name"
          style="margin-bottom: 30px"
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
    return {
      pokemonOfCurrentType: "",
      types: "",
      activeType: "rock"
    };
  },
  methods: {
    somethingHappened: function(name) {
      console.log("something happened");
      this.activeType = name;
      this.retrievePokemonOfSpecifiedType(this.activeType);
    },
    retrievePokemonOfSpecifiedType: function(type) {
      const axios = require("axios");
      const vm = this;
      axios({
        method: "get",
        url: "https://pokeapi.co/api/v2/type/" + type
      }).then(function(response) {
        // console.log(response.data.pokemon);
        vm.pokemonOfCurrentType = response.data.pokemon;
      });
    }
  },
  mounted: function() {
    console.log("mounted function ran");
    const axios = require("axios");
    const vm = this;
    this.retrievePokemonOfSpecifiedType(this.activeType);
    axios({
      method: "get",
      url: "https://pokeapi.co/api/v2/type"
    }).then(function(response) {
      // console.log(response.data.results);
      vm.types = response.data.results;
    });
  }
};
</script>

<style>
</style>
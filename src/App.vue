<template>
  <div id="app">
    <div class="container">
      <h1 class="text-center display-1"><span class="text-capitalize">{{ActiveType}}</span> on \m/</h1>
      <button
        v-on:click="SomethingHappened(element.name)"
        class="btn btn-primary"
        v-for="(element, index) in types"
        :key="index"
        style="margin-bottom: 30px"
      >{{element.name}}</button>
      <div class="row">
        <card
          :url="element.pokemon.url"
          v-for="(element, index) in pokemonOfRockType.pokemon"
          :key="index"
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
      pokemonOfRockType: "",
      types: "",
      ActiveType: ""
    };
  },
methods:{
  SomethingHappened: function(name){
    console.log(name)
    this.ActiveType = name
  }
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
    axios({
      method: "get",
      url: "http://pokeapi.co/api/v2/type/"
    }).then(function(response) {
      console.log(response.data);
      vm.types = response.data.results;
    });
  }
};
</script>


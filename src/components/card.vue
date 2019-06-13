<template>
  <div>
    <div class="card" style="width: 18rem;">
      <img class="card-img-top" v-bind:src='pokemon.sprites["front_default"]' alt="Card image cap">
      <div class="card-body">
        <h5 class="card-title">Name: {{pokemon.name}}</h5>
        <p class="pokemon-height">Height: {{pokemon.height * 3.937}}"</p>
        <p class="pokemon-weight">Weight: {{pokemon.weight}} units</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "card",
  data: function() {
    return { pokemon: "" };
  },
  props: {
    msg: String
  },
  mounted: function() {
    const axios = require("axios");
    const vm = this;
    axios({
      method: "get",
      url: "http://pokeapi.co/api/v2/pokemon/dratini"
    }).then(function(response) {
      console.log(response);
      vm.pokemon = response.data;
    });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

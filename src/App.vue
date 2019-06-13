<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Hello World"/>
    <card :url="item.pokemon.url" v-for="item in pokemonOfRockType" :key="item.pokemon.name"></card>
    <div v-for="item in pokemonOfRockType" :key="item.pokemon.name">
      {{ item.pokemon.name }}<br>
      {{ item.pokemon.url }}
      <br><br>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import card from './components/card.vue'

export default {
  name: 'type',
  components: {
    HelloWorld,
    card
  },
  data: function() {
    return {
        pokemonOfRockType: ""
    }
  },
  props: {
    url: String
  },
  mounted: function() {
    console.log("mounted function ran")
    const axios = require('axios');
    const vm = this;
    // Blastoise
    axios({
        method: 'get',
        url: 'http://pokeapi.co/api/v2/type/rock',
        responseType: 'stream'
    }) // end of axios
    .then(function (response) {
        console.log(response.data),
        vm.pokemonOfRockType = response.data.pokemon
    });
  }
} // end of function
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

<template>
  <div id="app">
    <div class="container">
      <!--m = margin-->
      <h1 class = "text-center display-1 m-5">{{ activeType }} Type Pokemon</h1>
      <span v-for="type in types" class="btn btn-primary m-1" v-on:click="somethingHappened(type.name)">
        {{ type.name }}
      </span>
      <div class="row"> 
        <card :url="item.pokemon.url" v-for="item in pokemonOfCurrentType" :key="item.pokemon.name"><br><br></card>
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import card from './components/card.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    card
  },
  data: function() {
    return {
        pokemonOfCurrentType: "",
        types: "",
        activeType: "Rock",
    }
  },
  methods: {
    somethingHappened: function(name) {
      console.log("something happened")
      this.activeType = name;
      this.retrievePokemonOfSpecifiedType(this.activeType);
    },
    retrievePokemonOfSpecifiedType: function(type) {
      const axios = require('axios');
      const vm = this;
      axios({
        method: 'get',
        url: 'http://pokeapi.co/api/v2/type/' + type,
        // responseType: 'stream'
    }) // end of axios
    .then(function (response) {
        // onsole.log(response.data),
        vm.pokemonOfCurrentType = response.data.pokemon
    });
    }
  },

  /* props: {
    url: String
  }, */
  mounted: function() {
    console.log("mounted function ran")
    const axios = require('axios');
    const vm = this;
    this.retrievePokemonOfSpecifiedType(this.activeType);
    axios({
      method: 'get',
      url: 'http://pokeapi.co/api/v2/type',
      // responseType: 'stream'
    }) // end of axios
    .then(function (response) {
      // console.log(response.data),
      vm.types = response.data.results
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

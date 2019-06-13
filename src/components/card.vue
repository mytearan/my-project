<template>
  <div class="hello">
    <div class="btn-group" role="group" aria-label="Basic example">
        <button type="button" class="btn btn-primary">abilities</button>
        <button type="button" class="btn btn-primary">moves</button>
        <button type="button" class="btn btn-primary">type</button>
    </div><br><br><br>
    <div class="card-deck">
      <div class="card" style="width: 18rem;">
        <img v-bind:src="pokemon.sprites.front_default" class="card-img-top" alt="pic of blastoise" width="15">
        <div class="card-body">
            <h5 class="card-title">{{ pokemon.name }}</h5>
            <!--<div>Height: {{ pokemon.height * 3.937 }} inches</div>-->
            <!--<div>Weight: {{ pokemon.weight }} units</div>-->
            <p class="card-text"><small class=".text-dark">Height: 16 inches<br>Weight: 855 pounds</small></p>
            <a id="button-secondary" href="#" class="btn btn-secondary">see moves</a>
        </div>
      </div>
    </div>
    <div class="card" style="width: 18rem;">
        <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/149.png" class="card-img-top" alt="pic of blastoise" width="15">
        <div class="card-body">
            <h5 class="card-title">{{ pokemon.name }}</h5>
            <p class="card-text"><small class=".text-dark">Height: 22 inches<br>Weight: 2100</small></p>
            <a id="button-secondary" href="#" class="btn btn-secondary">see moves</a>
        </div>
    </div>
  </div>
</template>
<!--git init/ git status/ git add ./get status/git commit -m "xxx"/git push/ git remote add origin/ git push-->
<script>
export default {
  height: 'card',
  
  name: 'card',
  data: function() {
    return {
        pokemon: ""
    }
  },
  props: {
    msg: String
  },
  mounted: function() {
    console.log("mounted function ran")
    const axios = require('axios');
    const vm = this;
    // Blastoise
    axios({
        method: 'get',
        url: 'http://pokeapi.co/api/v2/pokemon/blastoise',
        responseType: 'stream'
    }) // end of axios
    .then(function (response) {
        console.log(response.data);
        vm.pokemon = response.data
    }); // end of function
    // Dragonite
    axios ({
      method: 'get',
      url: 'http://pokeapi.co/api/v2/pokemon/dragonite',
      responseType: 'stream'
    }) // end of axios
        .then(function (response) {
        console.log(response.data);
        vm.pokemon = response.data
    });
  } // end of fundtion
}
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
#button-secondary {
    color: #ffffff;
}
</style>

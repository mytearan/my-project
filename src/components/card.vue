<template>
    <div class="col-3"><br>
      <div class="card" style="width: 18rem;">
        <img :src="pokemon.sprites.front_default" class="card-img-top" alt="pic of pokemon">
        <div class="card-body">
           <!-- <h1>{{url}}</h1> -->
            <h5 class="card-title text-capitalized">{{ pokemon.name }}</h5>
            <!-- <p class="card-text"> -->
            <div>Height: {{ pokemon.height * 3.937 }} inches<br></div>
            <div>Weight: {{ pokemon.weight }} units<br></div><br>
            <a id="button-secondary" href="#" class="btn btn-secondary">And I OOP</a>
        </div>
      </div>
    </div>
</template>
<!--git init/ git status/ git add ./get status/git commit -m "xxx"/git push/ git remote add origin/ git push/ GIT STATUS/ Git add . -->
<script>
export default {
  name: 'card',
  data: function() {
    return {
        pokemon: ""
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
        url: vm.url,
        responseType: 'stream'
    }) // end of axios
    .then(function (response) {
        console.log(response.data),
        vm.pokemon = response.data
    });
  }
} // end of function
</script>
<!--Add "scoped" attribute to limit CSS to this component only-->
<style scoped>
.card {
  text-align: center;
  margin-bottom: 30px;
}
/*
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
} */
#button-secondary {
  color: #ffffff;
}
</style>

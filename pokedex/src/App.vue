<template>
    <div class="container">
        <div class="row">
            <div class="col-md-3" v-for="(itemPokemon, index) in allPokemons" :key="index">
                <Pokemon :name="itemPokemon.name" :url="itemPokemon.url" :numId="index+1"/>
            </div>
        </div>
    </div>
</template>


<script>
import axios from 'axios';
import Pokemon from './components/Pokemon.vue';
export default {
  name:'App',
  data(){
    return {
      allPokemons:[]
    }
  },
  created() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=150&offset=0").then(retorno =>{
      console.log("Pegou a lista de pokemons");
      this.allPokemons = retorno.data.results;
    })
  },
  components:{
    Pokemon
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

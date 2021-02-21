<template>
  <div class="row">
    <div class="col-md-8 title">
      <h1>POKEDEX</h1>
      <p>
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam eu leo
        suscipit, scelerisque ligula vel, tincidunt felis
      </p>
    </div>
    <div class="col-md-4">
      <input
        type="search"
        class="form-control"
        placeholder="Pesquise pelo nome do pokemon"
        v-model="busca"
      />
    </div>
    <div
      class="col-md-3"
      v-for="(itemPokemon, index) in resultados"
      :key="index"
    >
      <Pokemon
        :name="itemPokemon.name"
        :url="itemPokemon.url"
        :numId="index + 1"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";

import Pokemon from "./Pokemon";

export default {
  name: "Index",
  components: {
    Pokemon,
  },
  data() {
    return {
      allPokemons: [],
      busca: "",
    };
  },
  computed: {
    resultados: function () {
      if (!this.busca.trim()) {
        return this.allPokemons;
      }

      return this.allPokemons.filter((resposta) => resposta.name == this.busca);
    },
  },
  created() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=150&offset=0")
      .then((retorno) => {
        this.allPokemons = retorno.data.results;
      });
  },
};
</script>
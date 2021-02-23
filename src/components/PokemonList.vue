<template>
  <v-container class="ma-auto">
    <v-layout row wrap justify-space-between>
      <Pokemon
        :pokemon="pokemon"
        :index="index + 1"
        v-for="(pokemon, index) in pokemonlist"
        :key="pokemon.url"
        @faveList="updateFaveList(index)"
      />

    </v-layout>
  </v-container>
</template>

<script>
import axios from "axios";
import Pokemon from "./Pokemon";
export default {
  name: "PokemonList",
  data() {
    return {
      pokemonlist: [],
      faveList: []
    };
  },
  created() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=15")
      .then((response) => (this.pokemonlist = response.data.results));
  },
  components: {
    Pokemon,
  },
  methods:{
    updateFaveList(e){
      if(!this.faveList.includes(e)){
          this.faveList.push(e);
      }else{
        let arr = this.faveList.filter(value => value !== e);
        this.faveList = arr;
      }
      
      console.log(e);
    }
  }
};
</script>

<style></style>

<template>
  <div class="home-view">
    <NavBar />
    <v-row rows="12">
      <v-col cols="12" lg="2" md="4" sm="6" v-for="pokemon in pokemons" :key="pokemon.name">
        <Cards :name="pokemon.data.name" :pokemonImg="pokemon.data.sprites.front_default" />
      </v-col>
    </v-row>
  </div>
</template>

<script>
import NavBar from '@/components/NavBar.vue';
import Cards from './components/Cards.vue';
import axios from 'axios';

export default {
  name: 'Home',
  components: { NavBar, Cards },
  data: () => ({
    pokemons: []
  }),
  methods: {
    getPokemons() {
      let endpoints = [];
      for (let i = 1; i < 100; i++) {
        endpoints.push(`https://pokeapi.co/api/v2/pokemon/${i}/`);
      }
      axios.all(endpoints.map((endpoint) => axios.get(endpoint))).then((response) => {
        console.log(response);
        this.pokemons = response;
      });
    }
  },
  mounted() {
    this.getPokemons();
  }
};
</script>

<style scoped>
.home-view {
  padding: 15px;
}
</style>

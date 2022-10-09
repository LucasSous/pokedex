<template>
  <div class="home-view">
    <NavBar v-model="search" @input="filter" />
    <v-row rows="12" v-if="pokemons.length">
      <v-col cols="12" lg="2" md="4" sm="6" v-for="pokemon in pokemons" :key="pokemon.name">
        <Cards :name="pokemon.data.name" :pokemonImg="pokemon.data.sprites.front_default" />
      </v-col>
    </v-row>
    <Loading v-if="isLoading" />
    <div v-if="search && !pokemons.length" class="d-flex justify-center">
      <h3>Nenum Pokemon encontrado!</h3>
    </div>
  </div>
</template>

<script>
import NavBar from '@/components/NavBar.vue';
import Cards from './components/Cards.vue';
import axios from 'axios';
import Loading from '@/components/Loading.vue';

export default {
  name: 'Home',
  components: { NavBar, Cards, Loading },
  data: () => ({
    pokemons: [],
    initalValues: [],
    isLoading: false,
    search: ''
  }),
  methods: {
    getPokemons() {
      this.isLoading = true;
      let endpoints = [];
      for (let i = 1; i < 300; i++) {
        endpoints.push(`https://pokeapi.co/api/v2/pokemon/${i}/`);
      }
      axios.all(endpoints.map((endpoint) => axios.get(endpoint))).then((response) => {
        this.pokemons = response;
        this.initalValues = response;
        this.isLoading = false;
      });
    },

    filter() {
      if (!this.search) {
        this.pokemons = this.initalValues;
        return;
      }
      const filter = this.initalValues.filter((item) =>
        item.data.name.toLowerCase().includes(this.search.toLowerCase())
      );
      this.pokemons = filter;
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

<template>
  <v-card class="mx-auto card">
    <v-img :src="pokemonImg" height="220px"></v-img>

    <v-card-title> {{ name }} </v-card-title>
  </v-card>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      default: ''
    },
    pokemonImg: {
      type: String,
      default: ''
    }
  }
};
</script>

<style>
.v-sheet.v-card {
  transition: all 0.3s ease;
  cursor: pointer;
}
.v-sheet.v-card:hover {
  background: rgb(223, 223, 223);
}
</style>

<template>
  <v-app-bar app color="#1c1c1c" dark hide-on-scroll height="80px">
    <v-row rows="12">
      <v-col cols="4" lg="8" class="d-flex align-center">
        <h2>Pokedex</h2>
      </v-col>
      <v-col cols="8" lg="4">
        <v-text-field
          label="Pesquisar Pokemon"
          prepend-inner-icon="mdi-magnify"
          filled
          dense
          :value="search"
          @input="($event) => $emit('input', $event)"
        ></v-text-field>
      </v-col>
    </v-row>
  </v-app-bar>
</template>

<script>
export default {
  props: {
    search: {
      type: String,
      default: ''
    }
  }
};
</script>

<style>
.v-text-field__details {
  display: none;
}
</style>

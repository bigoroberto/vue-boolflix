<template>
  <main class="container">
    <!-- inserisco il titolo in base al type -->
    <!-- richiamo titles -->
    <!-- utilizzo la bracket notation per ricevere la prop type -->
    <h1 class="text-center mt-3 mb-3">{{ titles[type] }}</h1>
    <div class="row d-flex justify-content-center mt-2 mb-2">
    <Card 
      v-for="card in list" 
      :key="card.id" 
      :card="card" 
    />
    </div>
  </main>
</template>

<script>
import Card from "./Card.vue";

export default {
  components: { Card },
  name: "Main",
  props: { // App passa a Main i seguenti dati
    type: String,
    list: Array,
  },
  data() {
    return {
      // creo un oggetto titles per visualizzare entrambi i titoli 
      titles: {
        movie: "Movies",
        tv: "TV Series",
      },
    };
  },
};
</script>

<style lang='scss' scoped>
</style>
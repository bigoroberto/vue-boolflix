<template>
  <div id="app">
    <!--  all'header (che mi ha passato con il $emit l'evento) gli restituisco l'evento con la funzione (callAPI)-->
    <Header @clickSearch ='callAPI'/>
    <!-- al main assegno (dando un props di nome listaFilm) l'arrFilm-->
    <Main :listaFilm = 'arrFilm'/>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Main from '@/components/Main.vue';

import axios from 'axios';

export default {
  name: 'App',
  components: { 
    Header,
    Main,
  },

  data(){
    return{
      apiURL: 'https://api.themoviedb.org/3/search/movie',
      apiKey: '883d759bdcf64cac4dd1122ba345f4b3',
      query: '',
      /* creo una var che mi prenda il risultato della chiamata API */
      arrFilm: [],
    }
  },
  methods : {
    /* creo la funzione che mi fa chiamare l'API ogni volta che ne ho bisogno */
    /* assegno la funzione callAPI all'header aggiungendo un searchText nelle tonde (che prenderà il valore del searchFilm) e alla query nei PARAMS */
    callAPI (searchText){
      axios.get(this.apiURL, {
        params:{
          api_key: this.apiKey,
          query: searchText,
          language : "it-IT"
        }
      })
      .then(res=>{
        console.log(res.data.results);
        /* uso l'array vuoto creato nel data, che richiamo con il this. per ricerevere il risultato della chiamata API */
        this.arrFilm = res.data.results;
      })
      .catch(err=>{
        console.log(err)
      })
    }
  },
  created(){
    //this.callApi();
  }
}
</script>

<style lang="scss">
   @import './assets/styles/generals';
</style>

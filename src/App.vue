<template> 
  <div id="app">

    <!-- all''evento $emit startSearch invoco la funzione startSearch -->
    <Header @startSearch ='startSearch'/>

    <!-- in caso di assenza di risultati visualizzo questo h1 -->
    <h1 v-if="results.movie.length === 0 && results.tv.length === 0">Nessun risultato trovato</h1>

    <!-- ho due componenti Main per movie e tv e li visualizzo solo se ci sono gli elementi nell'array -->
    <!-- passo due props: tipo di dato (movie o tv) e l'elenco dei risultati -->
    <Main v-if="results.movie.length > 0" type='movie' :list="results.movie" /> 
    <Main v-if="results.tv.length > 0" type='tv' :list="results.tv" /> 
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
      apiUrl: 'https://api.themoviedb.org/3/search/',
      apiKey: '883d759bdcf64cac4dd1122ba345f4b3',
      query: '',
      //in questo oggetto memorizzo le due ricerche
      results:{
        'movie':[],
        'tv':[],
      }
    }
  },
  methods : {

    //lancio la ricerca
    startSearch(obj){
      //resetto le ricerche passate
      this.resetResults();
      //se "CERCA TUTTO" faccio due chiamate
      if(obj.type === 'all'){
        this.getAPI(obj.text, 'movie');
        this.getAPI(obj.text, 'tv');
      }else{
        this.getAPI(obj.text, obj.type);
      }
    },

    resetResults(){
      this.results.movie = [];
      this.results.tv = [];
    },
    
    //funzione per la chiamata axios
    getAPI (query, type){

      //effettuo la chiamata solo se c'è un testo da cercare 
      if(query !== ''){
        axios.get(this.apiUrl + type, {
          params:{
            api_key: this.apiKey,
            query: query,
            language : "it-IT"
          }
        })
        .then(res=>{
          // in base al tipo di ricerca salvo il dato nell'array dell'oggetto results
          this.results[type] = res.data.results
          console.log(this.results);
        })
        .catch(err=>{
          console.log(err)
        })
      }
    }
  },
  created(){
    //this.getAPI('ritorno al futuro', 'movie', 'tv');
  }
}
</script>

<style lang="scss">
   @import './assets/styles/generals';
body {
  text-align: center;
  color: #2c3e50;
  
}
</style>

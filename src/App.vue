<template>
  <div id="app">

    <!-- all'eveto $emit startSearch invoco la funzione startSerach -->
    <Haed @startSearch="startSearch" />

    <!-- in caso di assenza di risultati visualizzo questo h1 -->
    <h1 v-if="results.movie.length === 0 && results.tv.length === 0">Nessun risultato trovato</h1>

    <!-- ho 2 componenti Main per movie e tv e li visualizzo solo se coi sono elementi nell'array -->
    <!-- passo 2 pros: tipo di dato (movie o tv) l'elenco dei risultati -->
    <Main v-if="results.movie.length > 0"  type='movie' :list="results.movie" />
    <Main v-if="results.tv.length > 0" type='tv' :list="results.tv"/>

  </div>
</template>

<script>
import Haed from './components/Haed';
import Main from './components/Main';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Haed,
    Main
  },
  data(){
    return{
      apiUrl: 'https://api.themoviedb.org/3/search/',
      apiKey: '1b3eb153fce73eb6b953f7d515b2dc1d',
      // in questo oggetto memorizzo le 2 ricerche
      results:{
        'movie':[],
        'tv':[]
      }
    }
  },
  methods:{

    // lancio la ricerca
    startSearch(obj){
      // resette le ricerche passate
      this.resetResults();
      // se "CERCA TUTTO" faccio 2 chiamate
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

    // funzione per la chiamata axios
    getAPI(query, type){
      
      // effettuo la chiamata solo se c'è un testo da cercare
      if(query !== ''){
        axios.get(this.apiUrl+type,{
            params:{
              api_key: this.apiKey,
              query: query,
              language: 'it-IT'
            }
          })
          .then(res => {
            // in base al tipo di ricerca slavo il dato nell'array delloggetto results
            this.results[type] = res.data.results;
            console.log('MOVIE',this.results.movie);
            console.log('TV', this.results.tv);
          })
          .catch(err => {
            console.log(err);
          })
      }
    }

  },
  created(){
    
      let type = 'movie'
      axios.get('https://api.themoviedb.org/3/movie/popular',{
          params:{
            api_key: this.apiKey,
            language: 'it-IT'
          }
        })
        .then(res => {
           this.results[type] = res.data.results;
        })
        .catch(err => {
          console.log(err);
        })
    
  }
}
</script>

<style lang="scss">
@import './assets/styles/general';

</style>

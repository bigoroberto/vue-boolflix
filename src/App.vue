<template> 
  <div id="app">
    <Header @startSearch ='startSearch'/>
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
      results:{
        'movie':[],
        'tv':[],
      }
    }
  },
  methods : {

    startSearch(obj){
      this.resetResults();
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
    
    getAPI (query, type){
      axios.get(this.apiUrl + type, {
        params:{
          api_key: this.apiKey,
          query: query,
          language : "it-IT"
        }
      })
      .then(res=>{
        this.results[type] = res.data.results
        console.log(this.results);
      })
      .catch(err=>{
        console.log(err)
      })
    }
  },
  created(){
    //this.getAPI('ritorno al futuro', 'movie', 'tv');
  }
}
</script>

<style lang="scss">
   @import './assets/styles/generals';
   body{
     background-color: darken($color: #0c5466, $amount: 0);
   }
</style>

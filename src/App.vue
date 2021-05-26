<template>
  <div id="app">
    <Header @clickSearch ='callApi'/>
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
      arrFilm: [],
    }
  },
  methods : {
    callApi (searchText){
      axios.get(this.apiURL, {
        params:{
          api_key: this.apiKey,
          query: searchText,
          language : "it-IT"
        }
      })
      .then(res=>{
        console.log(res.data.results);
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

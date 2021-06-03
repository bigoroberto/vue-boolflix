<template>
    <div id="app">
      <!-- richiamo evento custom nell'header che scatenerà la funzione searchMovies -->
        <Header
        @searchMovie= "searchMovies"
        :setDefault = setDefault
        />

        <h1 
        v-if="check()"
        class="text-center mt-5"
        >La ricerca non ha prodotto risultati</h1>
        
        <h1 
        v-if=" searched===false " 
        class="text-center mt-5"
        >FILM DEL MOMENTO</h1>

        <Main v-if="results.movie.length > 0" type="movie" :list= results.movie :searched= searched />

        <h1 
        v-if=" searched===false "
        class="text-center mt-5"
        >SERIE TV DEL MOMENTO</h1>

        <Main v-if="results.tv.length > 0" type="tv" :list= results.tv :searched= searched />

    </div>
</template>

<script>
/* import Vue from 'vue' */
import axios from 'axios';
import Header from './components/Header';
import Main from './components/Main'
/* import FlagIcon from 'vue-flag-icon'
Vue.use(FlagIcon); */

export default {
  name: 'App',
  components: {
    Header,
    Main
  },
  data(){
    return {
        apiUrl:"https://api.themoviedb.org/3/search/",
        apiKey: '4df959eab3283b1ac2c5a67b1e5247b9',
        results:{
            "movie":[],
            "tv":[]
        },
        searched:false
    }
  },
  created(){
    //richiamo le funzione due volte passando un parametro differente all'interno,in modo da avere sia film che serie tv alla creazione
    this.getPop("movie");
    this.getPop("tv");
            
        
  },
    methods:{
        //funzione per la condizione del v-if del primo titolo,se la ricerca non produrrà risultati allora sarà visibile
        check(){
            return this.searched && this.results.movie.length === 0 && this.results.tv.length === 0
        },
        //funzione per resettare gli array 
        reset(){
            this.results.movie= [];
            this.results.tv= [];
            this.searched=false;//resetto a false il dato in modo che il primo titolo verrà nascosto al momento del reset e renderà visibile film/serie popolari
        },
        //funzione per la situazione di default,viene passata come prop per il bottone reset
        setDefault(){
            this.reset();
            this.getPop("movie");
            this.getPop("tv");
        },
        //funziona che viene scatenata dal bottone cerca o dal keyup.enter ,passo come parametro l'oggetto che viene mandato tramite $emit
        searchMovies(obj){
            this.reset();//resetto in modo che se la ricerca restituisce un errore non rimangono gli elementi precedenti
            if(obj.type === "all" && obj.text !== ""){
                //passo manualmente il type,in modo da richiamare entrambe le funzioni
                this.getApi(obj.text, "movie");
                this.getApi(obj.text, "tv");
                this.searched=true;//una volta lanciata la funzione cambio il valore a true
            }else{
                //se la stringa di ricerca rimane vuota allora richiamo la situazione di default
                this.getPop("movie");
                this.getPop("tv");
            }
            
        },

        //funzione per ricavare i dati
        getApi(query, type){
            axios.get(this.apiUrl+type,{
                params:{
                    api_key: this.apiKey,
                    query: query,
                    language: "it-IT"
                }
            })
            .then(res => {
                    this.results[type] = res.data.results;
            })
            .catch(err => {
                console.log(err);
            })
            
        },
        //funzione per ricavare film e serie tv più popolari alla creazione dell'app
        getPop(typePop){
            axios.get("https://api.themoviedb.org/3/"+ typePop +"/popular",{
                params:{
                    api_key: this.apiKey,
                    language: "it-IT"
                }
            })
            .then(res => {
                this.results[typePop] = res.data.results;
            })
            .catch(err => {
                console.log(err);
            })
        }
    }
}
</script>

<style lang="scss">
@import './assets/styles/general.scss';
h1{
    text-shadow: 4px 4px 2px #000;
}
</style>
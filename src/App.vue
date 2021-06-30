<template>
  <div id="app">

    <!-- catturo l'evento search lanciato in header -->
    <Header 
      @search="search" 
    />

    <!-- aggiungo un contenitore con background e descrizione pagina che visualizzo solo all'accesso -->
    <!-- utilizzo una condizione -->
    <div 
      v-if="welcome"
      class="position-relative"
    >
      <div class="welcome"></div>
      <div class="mc_bool position-absolute">
        <h1>boolflix</h1>
        <h3>Film, serie TV e tanto altro.</h3>
      </div>
    </div>

    <!-- se show è true mostro l'h1 e il relativo messaggio -->
    <div class="d-flex justify-content-center align-items-center mc_msg">
      <h1 
        v-if='show'
        class="text-center"
      >
       nessun risultato trovato
      </h1>
      <!-- <h1 v-if='results.movie.length === 0 && results.movie.length === 0'>nessun risultato</h1> -->
    </div>

    <!-- vedo Main solo se l'array movie contiene qualcosa -->
    <!-- binding di results.movie -->
    <Main 
      v-if="results.movie.length > 0" 
      type="movie" 
      :list="results.movie" 
    />

    <!-- vedo Main solo se l'array tv contiene qualcosa -->
    <!-- binding di results.tv -->
    <Main 
      v-if="results.tv.length > 0" 
      type="tv" 
      :list="results.tv" 
    />
  </div>
</template>

<script>
// importo in app...
import axios from "axios";
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";

export default {
  name: "App",
  // dichiaro i componenti esportati in APP
  components: {
    Header,
    Main,
  },
  data() {
    return {
      apiURL: "https://api.themoviedb.org/3/search/",
      apiKey: "8aba2f0fc3e09fb1de7523aaaf3513bc",
      query: "",
      welcome: true, // se true mostro un elemento di default con background di 'benvenuto'. Dopo la chiamata API diventa false
      show: false, // utilizzo la variabile show per mostrare o no il messaggio 'nessun rislutato trovato'
      results: {  // oggetto che contiene due proprietà/array. Servono nel main per smistare i risultati in base al tipo
        movie: [],
        tv: [],
      },
    };
  },
  methods: {
    // funzione che richiama la funzione searching sia in movie che in tv
    // doppia chiamata API
    // obj è il secondo parametro passato nell'$emit (in header)
    search(obj) {
      if (obj.type === "all") {
        this.searching(obj.text, "movie");
        this.searching(obj.text, "tv");
      }
    },
    // funzione che permette di eseguire la chiamata API avviando la ricerca di query(del testo inserito dall'utente)
    searching(query, type) {
      // se query non è un campo vuoto...
      if (query != "") {
        this.query = query;
        this.show = false;
        // ... effetto la chiamata API
        axios
          .get(this.apiURL + type, {
            params: {
              api_key: this.apiKey,
              query: this.query,
              language: "it-IT",
            },
          })
          .then((resp) => {
            // ricevo la risposta
            // visualizzo la risposta nel relativo array di oggetti (movie o tv)
            this.results[type] = resp.data.results;
            console.log(this.results);
            // se non è stato trovato nessun risultato trasformo show in true.
            if(this.results.movie.length === 0 && this.results.tv.length === 0){
              this.show = true // v-if='show = true' mostra il messaggio 'Nessun risultato trovato'
            }
            this.welcome = false // non mostro più l'elemento di 'benvenuto'
          })
          .catch((error) => {
            console.log(error);
          });
      }
    },
  },
};
</script>

<style lang="scss">
// importo il foglio di stile general.scss
@import "./assets/style/general";
.welcome {
  width: 100%;
  height: 90vh;
  background-image: url('./assets/img/boolflix.png');
  filter: opacity(0.2);
}
.mc_bool {
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  h1 {
    font-size: 3em;
    color: $color-btn;
    text-transform: uppercase;
    text-shadow: 0px 3px 2px rgba(12, 10, 10, 0.767);
  }
  h3 {
    font-size: 3em;
  }
}
.mc_msg {
  height: 80vh;
  position: absolute;
  left: 50%;  
  transform: translate(-50%);
}
</style>

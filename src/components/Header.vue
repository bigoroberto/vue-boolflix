<template>
  <header class="d-flex justify-content-between align-items-center ps-5 pe-5">
    <div class="logo">
      <span>boolflix</span>
      <span>b</span>
    </div>
    <div>
      <form class="d-flex mt-3 mb-3">
        <div>
          <!-- con v-model faccio il binding di textToSearch, ovvero del testo inserito nell'input -->
          <!-- con @keyup.enter faccio partire la funzione startSearch premendo invio -->
          <input
            v-model.trim="textToSearch" 
            @keyup.enter="startSearch"
            class="form-control"
            type="text"
            placeholder="Find your movie/TV show"
          />
        </div>
        <div class="ms-3">
          <!-- al click sul bottone faccio partire la funzione startSearch-->
            <!-- .prevent evita che si ricarichi la pagina ogni volta che clicco -->
          <button 
            @click.prevent="startSearch" 
            class="btn btn-primary mc_btn"
          >
            Search
          </button>
        </div>
      </form>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    // in data carico la variabile textToSearch
    return {
      textToSearch: "",
    };
  },
  methods: {
    // funzione che fa partire la ricerca
    startSearch() {
      // $emit 'search' è un evento che viene letto dal padre (APP)
      // ho bisogno di due informazioni: il nome dell'evento (search) e un oggetto in cui ho il testo da cercare e il tipo di ricerca da effettuare
      this.$emit("search", {text: this.textToSearch, type: 'all'} );
      console.log(this.textToSearch);
      // svuoto la stringa di ricerca
      this.textToSearch = "";
    },
  },
};
</script>

<style lang='scss' scoped>
/* importo le variabili */
@import "../assets/style/vars.scss";
header {
  background: $color-header;
  height: 65px;
  div.logo {
    color: $color-btn;
    text-transform: uppercase;
    font-weight: 700;
    margin: 5px;
    margin-right: 10px;
    span{
      &:last-child {
       font-size: 2em;
      }
    }
  }
  .mc_btn {
    background-color: $color-btn;
    border-color: transparent;
    &:hover {
      filter: brightness(1.2);
    }
  }
}
@media only screen and (max-width: 450px) {
  button {
    display: none;
  }
  div.logo span:first-child {
    display: none;
  }
  div.logo span:last-child {
    display: block;
  }
}
@media only screen and (min-width: 451px) {
  div.logo span:last-child {
    display: none;
  }
}

</style>
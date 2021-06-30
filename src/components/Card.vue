<template>
  <ul class="m-3 p-2 p-2">

    <li>
      <span>Title: </span>
      <!-- a secoda che si cerchi un film o una serie tv inserisco entrambi i percorsi da visualizzare.
        film e serie tv hanno campi di risposta differenti (title e name) 
        Utilizzo un 'or logico ||'-->
      <h2>{{ card.title || card.name }}</h2>
    </li>

    <li>
      <span>Original Title: </span>
      <!-- a secoda che si cerchi un film o una serie tv inserisco entrambi i percorsi da visualizzare.
        film e serie tv hanno campi di risposta differenti (original_title e original_name) 
        Utilizzo un 'or logico ||'-->
      <h3>{{ card.original_title || card.original_name }}</h3>
    </li>

    <li>
      <span class="d-block">Original Language: </span>
      <h4 class="d-inline">{{ card.original_language }}</h4>
      <!-- se original_language è uguale a 'en' o 'it' aggiungo l'immagine di una bandierina -->
      <!-- binding di src che concatena il percorso dell'immagine + original_language + estensione immagine-->
      <!-- img-fluid rende responsive l'immagine -->
      <img
        v-if="
          card.original_language === 'en' || card.original_language === 'it'
        "
        :src="require(`../assets/img/flag-${card.original_language}.png`)"
        :alt="'flag-' + card.original_language"
        class="img-fluid"
      />
      <!-- percorso alternativo :src img -->
      <!-- :src="require('../assets/img/flag-'+[card.original_language]+'.png')"  -->
    </li>

    <li>
      <span>Vote Average: </span>
      <!-- se vote_average non è una stringa vuota... -->
      <!-- richiamo la funzione che arrotonda vote.average e lo trasforma in un numero da 1 a 5 -->
      <!-- con position mostro 5 stelle vuote e sopra tante stelle piene in base al voto-->
      <!-- <h4>{{getCeil(card.vote_average)}} </h4> -->
      <!-- {{card.vote_average/2}} -->
      <div 
      v-if="card.vote_average != ''"
      class="star">
        <div class="star_empty">
          <i class="far fa-star"></i>
          <i class="far fa-star"></i>
          <i class="far fa-star"></i>
          <i class="far fa-star"></i>
          <i class="far fa-star"></i>
        </div>
        <div class="star_full">
        <!-- stampo direttamente tante stelline quanto è il numero del voto con un v-for -->
          <i
            v-for="(star, index) in getCeil(card.vote_average)"
            :key="index"
            class="fas fa-star"
          >
          </i>
        </div>
      </div>
    </li>

    <li>
      <span>Overview: </span>
      <!-- richiamo la funzione che taglia la stringa dopo un n numeri di caratteri aggiungendo ...-->
      <p>
        {{ substringText() }} 
      </p>
    </li>

    <!-- aggiungo l'immaginde di copertina... -->
    <!-- <img :src="('https://image.tmdb.org/t/p/w342'+[card.poster_path])" alt=""> -->
    <!-- solo se l'oggetto ha un'immagine di coperina -->
    <img
      v-if="card.poster_path"
      class="img-fluid mc_poster"
      :src="getUrl()"
      :alt="`poster ${card.original_title}`"
    />

  </ul>
</template>

<script>
export default {
  name: "Card",
  props: {
    // Main.vue passa a Card.vue i seguenti dati...
    card: Object,
  },
  methods: {
    // funzione per trasformare il voto in numero intero da 1 a 5
    getCeil(num) {
      let n = Math.ceil(num) / 2;
      return Math.ceil(n);
    },
    // funzione che restituisce il percorso dell'immagine poster
    getUrl() {
      let url = "https://image.tmdb.org/t/p/w342";
      let path = [this.card.poster_path];
      return url + path;
    },
    // funzione che fa visulaizzare solo i primi 100 caratteri di un testo aggiungendo alla fine '...'
    substringText() {
      return this.card.overview.substring(0, 100) + "...";
    },
  },
};
</script>

<style lang="scss" scoped>
// importo le variabili
@import "../assets/style/vars.scss";
ul {
  box-shadow: 0px 0px 3px white;
  position: relative;
  background-color: $color-header;
  list-style: none;
  cursor: pointer;
  transition: all 0.8s;
  margin-bottom: 50px;
  padding: 30px;
  height: 350px;
  overflow-y: hidden;
  overflow-wrap: break-word;
  flex-grow: 0;
  flex-shrink: 1;
  flex-basis: 230px;
  &:hover {
    filter: brightness(1.4);
    transform: scale(1.1);
  }
  li {
    text-overflow: ellipsis;
    overflow: hidden;
    span {
      color: $color-btn;
      font-size: 0.8em;
      text-transform: uppercase;
    }
    h2,
    h3,
    h4 {
      font-size: 0.9em;
    }
    p {
      font-size: 0.9em;
    }
    img {
      height: 1.5rem;
      padding-bottom: 7px;
      margin-left: 7px;
    }
    div.star {
      position: relative;
      .star_empty {
        position: absolute;
        color: darkgoldenrod;
      }
      .star_full {
        color: darkgoldenrod;
      }
      }
  }
  img.mc_poster {
    display: block;
    position: absolute;
    top: 0%;
    left: 0;
    height: 100%;
    width: 100%;
    transition: all 0.6s;
    &:hover {
      filter: opacity(0);
    }
  }
}
</style>
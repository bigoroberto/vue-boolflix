<template>
<main> 
  <!-- adesso ciclo l'array per avere ogni singolo elemento per poi stamparlo a video -->
  <div v-for="(film, index) in listaFilm"
      :key="index">
      <ul>
        <li>
        <h3>Titolo del film:  {{film.title}}</h3>
        </li>
        <li>
        <h3>Titolo originale:  {{film.original_title}}</h3>
        </li>
        <li>
        <h3>Lingua originale:  {{film.original_language}}</h3>
        </li>
        <li>
        <h3>Voto:  {{film.vote_average}}</h3>
        </li>
      </ul>
  </div>
</main>
</template>

<script>
export default {
  name:'Main',
  /* con il props listaFilm preparo il main ad accogliere quello che gli passerò */
  /* listaFilm sarà il mio nuovo array di film */
  props:{
    listaFilm: Array
  }
}
</script>

<style>

</style>
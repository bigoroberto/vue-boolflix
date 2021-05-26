<template>
<main> 
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
  props:{
    listaFilm: Array
  }
}
</script>

<style>

</style>
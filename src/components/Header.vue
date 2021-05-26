<template>
  <header>
    <!-- assegno al keyup e al click un $emit, quindi passerò al padre un evento "clickSearch" con un valore (searchFilm) -->
    <input type="text"
            @keyup.enter='$emit("clickSearch", searchFilm)'
            v-model="searchFilm">
    <button
      @click='$emit("clickSearch", searchFilm)'
      >
      SEARCH
    </button>
  </header>
</template>

<script>
export default {
  name:'Header',
  data(){
    return{
      /* creo una variabile searchFilm che di base lascio vuota e che prenderà poi il valore del v-model */
      searchFilm : '',
    }
  }
}
</script>

<style>

</style>
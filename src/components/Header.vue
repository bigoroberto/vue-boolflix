<template>
  <header>
    <input type="text"
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
      searchFilm : '',
    }
  }
}
</script>

<style>

</style>
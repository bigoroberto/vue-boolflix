<template>
<main class="container"> 
  <!-- mostro a video il titolo relativo al type -->
  <h1>{{titles[type]}}</h1>
  <div class="copertina">
    <!-- ciclo la lista dei risultati  -->
    <Card 
      v-for="card in list"
      :key="card.id"
      :card="card"
      />
  </div>
</main>
</template>

<script>
import Card from '@/components/Card';

export default {
  name:'Main',
  components:{
    Card,
  },
  props:{
    type: String,
    list: Array,
  },
  data(){
    return{
      titles:{
        'movie': 'Film trovati',
        'tv': 'Serie tv trovate',
      }
    }
  }
}
</script>

<style lang="scss" scoped>

.copertina{
  display: flex;
}

</style>
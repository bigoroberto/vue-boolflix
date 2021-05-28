<template>
<main class="container"> 
  <h1>{{titles[type]}}</h1>
  {{list.length}}
  <Card 
    v-for="card in list"
    :key="card.id"
    :card="card"
    />
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

</style>
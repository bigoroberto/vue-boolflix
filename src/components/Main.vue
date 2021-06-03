<template>
  <main class="container">
    <!-- mostro a video il titolo realitvo al type -->
    <h1>{{ titles[type] }}</h1>

      <VueSlickCarousel v-bind="settings">
        <Card
            v-for="card in list"
            :key="card.id"
            :card="card"
          />
      </VueSlickCarousel>

    <!-- ciclo la lista dei risultati in Card -->
        
      
  </main>
</template>

<script>
import Card from '@/components/Card';
import VueSlickCarousel from 'vue-slick-carousel';
import 'vue-slick-carousel/dist/vue-slick-carousel.css';
import 'vue-slick-carousel/dist/vue-slick-carousel-theme.css';

export default {
  name: 'Main',
  components:{
    Card,
    VueSlickCarousel 
  },
  props:{
    type: String,
    list: Array
  },
  data(){
    return{
      titles:{
        'movie': 'Film',
        'tv': 'Serie',
      },
       settings:{
                "centerMode": true,
                "centerPadding": "10%",
                "focusOnSelect": true,
                "infinite": true,
                "slidesToShow": 4,
                "speed": 500,
                "responsive": [
                    {
                    "breakpoint": 1300,
                    "settings": {
                        "slidesToShow": 3
                    }
                    },
                    {
                    "breakpoint": 900,
                    "settings": {
                        "slidesToShow": 3,
                        "centerPadding": "5%",
                        "arrows":false
                    }
                    },
                    {
                    "breakpoint": 700,
                    "settings": {
                        "slidesToShow": 2,
                        "centerPadding": "15%",
                        "arrows":false
                    }
                    },
                    {
                    "breakpoint": 550,
                    "settings": {
                        "slidesToShow": 2,
                        "centerPadding": "5%",
                        "arrows":false
                    }
                    },
                    {
                    "breakpoint": 450,
                    "settings": {
                        "slidesToShow": 1,
                        "centerPadding": "20%",
                        "arrows":false
                    }
                    },
                    {
                    "breakpoint": 375,
                    "settings": {
                        "slidesToShow": 1,
                        "centerPadding": "15%",
                        "arrows":false
                    }
                    }
                ]
            }
      
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
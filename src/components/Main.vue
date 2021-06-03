<template>
  <main>
    
    <div class=" wrap p-5">
        <h1 v-if="searched" class="text-center mb-5">{{ titles[type].toUpperCase() }}</h1>
        <!-- componente slider e all'interno inserisco le card -->
        <VueSlickCarousel v-bind="settings">
            <Card
            v-for= "card in list" 
            :key= "card.id"
            :card = card
            />
        </VueSlickCarousel>
    </div>

  </main>
</template>

<script>
import Card from './Card';
//importo lo slider installato
import VueSlickCarousel from 'vue-slick-carousel'
import 'vue-slick-carousel/dist/vue-slick-carousel.css'
import 'vue-slick-carousel/dist/vue-slick-carousel-theme.css'

export default {
    name:'Main',
    components:{
        Card,
        VueSlickCarousel 
    },
    props:{
        type: String,
        list: Array,
        searched:Boolean,
    },
    data(){
        return{
            //sfruttando il type inserito nel tag del main andrò a cambiare in modo dinamico il titolo
            titles:{
                'movie': 'Film trovati',
                'tv': 'Serie tv trovate'
            },
            //impostazioni per lo slider
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
.wrap{
    max-width: 1920px;
    margin: 0 auto;
}
</style>
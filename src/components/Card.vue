<template>
<!--   <div class="p-3">
    <ul class="list-group">
      <li class="list-group-item">{{ card.title}}</li>
      <li class="list-group-item">{{ card.original_title  || card.original_name}}</li>
      <li class="list-group-item">{{ card.original_language }}</li>
      <li class="list-group-item">{{ card.vote_average }}</li>
    </ul>
  </div> -->
    <div class="p-3">
    <!-- <ul class="list-group">
      <li class="list-group-item">{{ card.title}}</li>
      <li class="list-group-item">{{ card.original_title  || card.original_name}}</li>
      <li class="list-group-item">{{ card.original_language }}</li>
      <li class="list-group-item"> <flag :iso="bandiere()" /></li>
      <li class="list-group-item">{{ Math.round(card.vote_average / 2) }}</li>
      <div
      v-for= 'index in 5'
      :key= 'index'
      >
        <i class="fas fa-star"
        v-if= "index <= Math.round(card.vote_average / 2)"
        ></i>
        <i class="far fa-star"
        v-else
        ></i>
      </div>
    </ul>
    <img :src="'https://image.tmdb.org/t/p/w300'+ card.poster_path " alt=""> -->
    <!-- fare img in script -->

    <div class="flip-card">
      <div class="flip-card-inner">
        <div class="flip-card-front">
          <img
            :src="'https://image.tmdb.org/t/p/w300' + card.poster_path"
            alt=""
            style="width:300px;height:400px;"
          />
        </div>
        <div class="flip-card-back">
          <p class="">Titolo: {{ card.title }}</p>
          <p class="">
            Titolo originale: {{ card.original_title || card.original_name }}
          </p>
          
          <!-- <p class="">{{ card.original_language }}</p> -->
          <p class=""><flag :iso="bandiere()" /></p>
          <!-- <p class="">{{ Math.round(card.vote_average / 2) }}</p> -->
          <div class="star" v-for="index in 5" :key="index">
            <i
              class="fas fa-star"
              v-if="index <= Math.round(card.vote_average / 2)"
            ></i>
            <i class="far fa-star" v-else></i>
          </div>
          <p class="">Overview: {{ card.overview }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props:{
    card:Object
  },
  methods:{
    bandiere(){
      if(this.card.original_language === 'en'){
        return "gb";
      }else{
        return this.card.original_language;
      }
    }
  }
}
</script>

<style lang="scss" scoped>
/* div, ul, li{
  background-color: brown;
}

div{
  margin-bottom: 20px;
}
i{
  display: inline-block;
} */

.flip-card {
  background-color: transparent;
  width: 300px;
  height: 400px;
  perspective: 1000px;
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.6s;
  transform-style: preserve-3d;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
}

.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

.flip-card-front,
.flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
}

.flip-card-front {
  background-color: #bbb;
  color: black;
}

.flip-card-back {
  overflow-y: auto;
  background-color: black;
  color: white;
  transform: rotateY(180deg);

}

.star {
  display: inline-block;
}
i {
  color: yellow;
}
</style>
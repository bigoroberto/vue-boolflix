<template>
  <header>

    <div class="d-flex pt-3 justify-content-between px-3">
      <div>
        <img src="https://fontmeme.com/permalink/210528/323aa9a77404d38b71457254b1d10499.png" alt="Boolflix">
      </div>
      <div class="form d-flex px-3">
        <div class="flex-grow-1">
          <input 
          v-model.trim="textToSearch"
          @keyup.enter="sendEmit()"
          placeholder="Cerca..."
          class="form-control"
          type="text" />

        </div>
        <div>
          <!-- all'$emit invio un oggetto con 2 parametri, il testo da cercare e il tipo di ricerca da fare -->
          <select class="form-select mx-3 "
              v-model="typeSelected"
              @change="sendEmit()">
            <option value="all">All</option>
            <option value="movie">Film</option>
            <option value="tv">Tv</option>
          </select>
        </div>
  
          
 

      </div>

    </div>
    
  </header>
</template>

<script>
export default {
  name: 'Header',
  data(){
    return{
      textToSearch: '',
      typeSelected: 'all'
    }
  },
  methods:{
    sendEmit(){
      this.$emit('startSearch',{text:this.textToSearch, type:this.typeSelected})
    },
  }
}
</script>

<style lang="scss" scoped>
header{
  height: 70px;
  background-image:linear-gradient(#000 ,#383838) 
}
img{
  width: 100px;
}
.form{
  flex-basis: 50%;
}
</style>
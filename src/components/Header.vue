<template>
  <header>
    <div class="container d-flex pt-3">
      <div class="flex-grow-1">
        <input
          v-model="textToSearch"
          @keyup.enter="$emit('startSearch', {text:textToSearch, type:'all'})"
          placeholder="Cerca film o serie tv"
          class="form-control"
          type="text" />
      </div>
      <div>
        <!-- all'$emit invio un oggetto con due parametri, il testo da cercare ed il tipo di ricerca da fare -->
        <button 
        @click="$emit('startSearch', {text:textToSearch, type:'movie'})" 
        class="btn btn-primary ms-3">CERCA FILM</button>
      </div>
      <div>
        <button 
        @click="$emit('startSearch', {text:textToSearch, type:'tv'})" 
        class="btn btn-primary ms-3">CERCA SERIE</button>
      </div>
      <div>
        <button 
        @click="$emit('startSearch', {text:textToSearch, type:'all'})" 
        class="btn btn-primary ms-3">CERCA TUTTO</button>
      </div>

    </div> <!-- chiusura container -->
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      textToSearch: "",
    };
  },
};
</script>

<style lang="scss" scoped>

header{
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 70px;
  background-color: black ;
  border-bottom: 3px solid red;
}

h1{
  margin-left: 10px;
  color: red;
}

input{
 outline:none;
}

button {
  background-color: red;
  border: 1px solid red;
  color: black;
  border-radius: 5px;
  padding: 5px;
  &:hover {
    color: red;
    transition: 1s;
    background-color: black;
    border: 1px solid red;
    border-radius: 5px;
  }
} 
</style>

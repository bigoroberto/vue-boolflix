<template>
  <header>
    <div class="container d-flex pt-3">
      <div class="flex-grow-1">
        <input
          v-model="textToSearch"
          placeholder="Cerca..."
          class="form-control"
          type="text" />
      </div>
      <div>
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
header {
  height: 70px;
  background-color: cornflowerblue;
}
</style>
<template>
  <div class="p-3">
    <ul class="list-group">
      <li class="list-group-item">{{card.title}}</li>
      <li class="list-group-item">{{card.original_title}}</li>
      <li class="list-group-item">{{card.original_language}}</li>
      <li class="list-group-item">{{card.vote_average}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name:'Card',
  props:{
    card:Object
  }
}
</script>

<style lang="scss" scoped>

</style>
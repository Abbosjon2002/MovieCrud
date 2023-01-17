<template>
<div class="app_info">
  <p class="fs-3 text-uppercase">Total movies: {{ countAllMovies }}</p>
  <p class="fs-4 text-uppercase">Favourite movies: {{ favourites }}</p>
</div>
</template>

<script>
export default {
  name: "AppInfo",
  props: {
    countAllMovies: {
      type: Number,
      required: true
    },
    favourites: {
      type: Number,
      required: true
    }
  }
}
</script>

<style scoped>
.app_info{
  padding: 1.5rem;
  border-radius: 4px;
  background-color: #fcfaf5;
  box-shadow: 0 10px 15px #00000030;

}
</style>
<template>
  <ul class="movie-list list-group">
    <MovieListItem/>
    <MovieListItem/>
    <MovieListItem/>
    <MovieListItem/>
  </ul>
</template>

<script>
import MovieListItem from "../movie-list-item/MovieListItem.vue";

export default {
  name: "MovieList",
  components: {MovieListItem}
}
</script>

<style scoped>
.movie-list{
  margin: 2rem 0 0;
  padding: 1.5rem;
  border-radius: 4px;
  background-color: #fcfaf5;
  box-shadow: 0 10px 15px #00000030;
}
</style>
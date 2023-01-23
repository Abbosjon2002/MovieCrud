<template>
  <ul class="movie-list list-group">
    <div v-if="movies.length <= 0">Yuklanmoqda </div>
    <MovieListItem v-for="movie in movies" :movie="movie" :key="movie.id" @onToggle="$emit('onToggle', $event)" @removeItem="$emit('removeItem', movie.id)"/>
  </ul>
</template>

<script>
import MovieListItem from "../movie-list-item/MovieListItem.vue";

export default {
  name: "MovieList",
  components: {MovieListItem},
  props: {
    movies: {
      type: Array,
      required:true
    }
  }
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
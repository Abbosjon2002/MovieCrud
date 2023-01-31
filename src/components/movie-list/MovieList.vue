<template>
  <ul class="list-group">
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

</style>
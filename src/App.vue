<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo :countAllMovies="movies.length" :favourites="movies.filter(e => e.favourite === true).length"/>

      <div class="search_panel">
        <SearchPanel/>
        <AppFilter/>
      </div>
      <MovieList :movies="movies"/>
      <MovieAddForm @createMovie="addNewMovie"/>
    </div>
  </div>
</template>

<script>
import AppInfo from "./components/app-info/AppInfo.vue";
import AppFilter from "./components/app-filter/AppFilter.vue";
import SearchPanel from "./components/search-panel/SearchPanel.vue";
import MovieList from "./components/movie-list/MovieList.vue";
import MovieAddForm from "./components/movie-add/MovieAddForm.vue";

export default {
  data() {
    return {
      title: "hello",
      movies: [
        {
          name: "Flash",
          viewers: 971,
          favourite: false,
          like: false,
          id: 1
        },
        {
          name: "Spidermon",
          viewers: 9717,
          favourite: false,
          like: false,
          id: 2
        },
        {
          name: "Capin Halal",
          viewers: 97,
          favourite: true,
          like: false,
          id: 3
        },
        {
          name: "Sheyx Tanos",
          viewers: 77,
          favourite: false,
          like: true,
          id: 4
        },
      ]
    }
  },
  components: {
    MovieAddForm,
    MovieList,
    SearchPanel,
    AppFilter,
    AppInfo

  },
  methods: {
    addNewMovie(item){
      this.movies.push(item)
    }
  }
}
</script>
<style>
.app {
  height: 100vh;
  color: #000000;
}

.content {
  width: 1000px;
  min-height: 700px;
  background-color: #000031;
  margin: 0 auto;
  padding: 5rem 1rem;
}

.search_panel {
  margin: 2rem 0 0;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 0 10px 15px #00000030;

}
</style>
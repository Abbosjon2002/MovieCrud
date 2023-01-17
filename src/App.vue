<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo/>

      <div class="search_panel">
        <SearchPanel/>
        <AppFilter/>
      </div>
      <MovieList />
      <MovieAddForm />
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
      title: "hello"
    }
  },
  components: {
    MovieAddForm,
    MovieList,
    SearchPanel,
    AppFilter,
    AppInfo

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

.search_panel{
  margin: 2rem 0 0;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 0 10px 15px #00000030;

}
</style>
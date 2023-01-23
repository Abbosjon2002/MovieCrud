<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo :countAllMovies="movies.length" :favourites="movies.filter(e => e.favourite === true).length"/>

      <div class="search_panel">
        <SearchPanel @updateTerm="updateTermHandler"/>
        <AppFilter @updateFilter="updateFilter" :filterName="filter"/>
      </div>
      <MovieList :movies="onFilterHandler(onSearchHandler(movies, term), filter)" @onToggle="onToggleHandler"
                 @removeItem="removeItemHandler"/>
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
import axios from "axios";
import BoxUI from "./ui-components/BoxUI.vue";
import PrimaryBtn from "./ui-components/PrimaryBtn.vue";

export default {
  components: {
    PrimaryBtn,
    BoxUI,
    MovieAddForm,
    MovieList,
    SearchPanel,
    AppFilter,
    AppInfo
  },
  data() {
    return {
      title: "hello",
      term: '',
      filter: '',
      res: '',
      movies: []
    }
  },


  methods: {
    addNewMovie(item) {
      this.movies.push(item)
    },

    onToggleHandler({id, prop}) {
      this.movies = this.movies.map(item => {
        if (item.id == id) {
          return {...item, [prop]: !item[prop]}
        }
        return item
      })
    },

    removeItemHandler(id) {
      this.movies = this.movies.filter(c => c.id !== id)
    },

    onSearchHandler(arr, term) {
      if (term.length == 0) {
        return arr
      }
      return arr.filter(c => c.name.toLowerCase().indexOf(term) > -1)
    },

    onFilterHandler(arr, filter) {
      switch (filter) {
        case 'popular':
          return arr.filter(c => c.favourite)
        case  'mostViewers':
          return arr.filter(c => c.viewers > 500)
        default:
          return arr
      }
    },

    updateTermHandler(term) {
      this.term = term
    },

    updateFilter(filter) {
      this.filter = filter
    },

    async fetchMovie() {
      try {
        setTimeout(async ()=>{
          const {data} = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
          const newArr = data.map(item => ({
            id: item.id,
            name:item.title,
            like: false,
            favourite: false,
            viewers: item.id*10
          }))
          this.movies = newArr
        },3000)
        } catch (error) {
        alert(error.message)
      }

    }
  },

  mounted() {
    this.fetchMovie()
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
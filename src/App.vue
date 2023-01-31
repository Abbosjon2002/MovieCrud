<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo :countAllMovies="movies.length" :favourites="movies.filter(e => e.favourite === true).length"/>

      <BoxUI class="search_panel">
        <SearchPanel @updateTerm="updateTermHandler"/>
        <AppFilter @updateFilter="updateFilter" :filterName="filter"/>
      </BoxUI>

      <BoxUI class="d-flex justify-content-center">

        <BoxUI v-if="!movies.length && !isLoading">No movies, yet!</BoxUI>
        <Loading v-else-if="isLoading" class="text-primary"/>
        <MovieList :movies="onFilterHandler(onSearchHandler(movies, term), filter)" @onToggle="onToggleHandler"
                   @removeItem="removeItemHandler"/>

      </BoxUI>

      <BoxUI class="d-flex justify-content-center">
        <nav aria-label="...">
          <ul class="pagination pagination-sm">
            <li v-for="pagenumber in totalPages" :key="pagenumber" @click="changePageNumber(pagenumber)"
                class="page-item" :class="{'active': page=== pagenumber}"><span class="page-link">{{
                pagenumber
              }}</span>
            </li>
          </ul>
        </nav>
      </BoxUI>
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
import Loading from "./ui-components/Loading.vue";

export default {
  components: {
    Loading,
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
      movies: [],
      isLoading: false,
      limit: 10,
      page: 1,
      totalPages: 0
    }
  },


  methods: {
    async addNewMovie(item) {
      try {
        const response = await axios.post('https://jsonplaceholder.typicode.com/posts', item)
        this.movies.push(response.data)
      }catch (error){
        alert(error.message)
      }
    },

    onToggleHandler({id, prop}) {
      this.movies = this.movies.map(item => {
        if (item.id == id) {
          return {...item, [prop]: !item[prop]}
        }
        return item
      })
    },

    async removeItemHandler(id) {
      try {
      const response = await axios.delete(`https://jsonplaceholder.typicode.com/posts/${id}`)
      this.movies = this.movies.filter(c => c.id !== id)
      }catch (error){
        alert(error.message)
      }

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
        this.isLoading = true;
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
          params: {
            _limit: this.limit,
            _page: this.page,
          }
        })
        const newArr = response.data.map(item => ({
          id: item.id,
          name: item.title,
          like: false,
          favourite: false,
          viewers: item.id * 10
        }))
        this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
        this.movies = newArr
      } catch (error) {
        alert(error.message)
      } finally {
        this.isLoading = false
      }

    },
    changePageNumber(page) {
      this.page = page
    }
  },

  mounted() {
    this.fetchMovie()
  },

  watch: {
    page() {
      this.fetchMovie()
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
  margin: 2rem 0;

}
</style>
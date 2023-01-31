<template>
  <BoxUI class="movie-add-form" :class="[]">
    <h3>Add new </h3>
    <form class="add-form d-flex gap-3" @submit.prevent>
      <input type="text" class="form-control new-movie-label" placeholder="Title of movie?" v-model="name">
      <input type="number" class="form-control new-movie-label" placeholder="Watched..." v-model="viewers">
      <PrimaryBtn class="btn-primary col-2" @click="addNewMovie">add +</PrimaryBtn>
    </form>
  </BoxUI>
</template>

<script>


export default {
  name: "MovieAddForm",
  data() {
    return {
      name: '',
      viewers: ''
    }
  },

  methods: {
    addNewMovie() {
      if (!this.name || !this.viewers) return
      const newMovie = {
        name: this.name,
        viewers: this.viewers,
        favourite: false,
        like: false,
      }
      this.$emit('createMovie', newMovie)
      this.name = ''
      this.viewers = ''
    },
  },
}
</script>

<style scoped>
.movie-add-form {
  margin: 2rem 0 0;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 0 10px 15px #00000030;
}


</style>
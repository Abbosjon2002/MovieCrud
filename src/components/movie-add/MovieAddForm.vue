<template>
<div class="movie-add-form">
  <h3>Add new </h3>
  <form class="add-form d-flex gap-3">
    <input type="text" class="form-control new-movie-label" placeholder="Title of movie?">
    <input type="text" class="form-control new-movie-label" placeholder="Watched...">

    <button class="btn btn-primary col-2">add +</button>
  </form>
</div>
</template>

<script>
export default {
  name: "MovieAddForm"
}
</script>

<style scoped>
.movie-add-form{
  margin: 2rem 0 0;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 0 10px 15px #00000030;
}
</style>
<template>
<BoxUI>
  <p class="fs-3 text-uppercase">Total movies: {{ countAllMovies }}</p>
  <p class="fs-4 text-uppercase">Favourite movies: {{ favourites }}</p>
</BoxUI>
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

</style>
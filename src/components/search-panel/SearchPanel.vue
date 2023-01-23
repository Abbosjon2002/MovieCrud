<template>
  <input type="text" class="form-control seach-input" placeholder="Search movies..." v-model="term" @input="$emit('updateTerm', term)">
</template>

<script>
export default {
  name: "SearchPanel",
  data(){
    return{
      term: ''
    }
  },

}
</script>

<style scoped>
.seach-input{
  margin: 1rem 0;
  padding: 1rem;
}
</style>
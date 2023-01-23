<template>
  <div class="btn-group d-flex">
    <PrimaryBtn v-for="btn in filterButtons"  :key="btn.name" :class="[filterName === btn.name ? 'btn-dark' : 'btn-outline-dark' ]"
            @click="updateFilter(btn.name)">{{ btn.title }}
    </PrimaryBtn>
  </div>

</template>

<script>

import PrimaryBtn from "../../ui-components/PrimaryBtn.vue";

export default {
  name: "AppFilter",
  components: {PrimaryBtn},
  props: {
    filterName: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      filter: '',
      filterButtons: [
        {
          title: 'All',
          name: 'all'
        },
        {
          title: 'Popular',
          name: 'popular'
        },
        {
          title: 'Most viewed',
          name: 'mostViewers'
        },
      ],
    }
  },
  methods: {
    updateFilter(filter) {
      this.filter = filter
      this.$emit('updateFilter', this.filter)
    }
  }
}
</script>

<style scoped>

</style>
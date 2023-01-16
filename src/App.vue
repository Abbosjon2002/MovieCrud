<template>
  <div class="app">
    <div class="content">
      <AppInfo/>
      <AppFilter/>
    </div>
  </div>

  <h1>{{ title }}</h1>

</template>

<script>
import AppInfo from "./components/app-info/AppInfo.vue";
import AppFilter from "./components/app-filter/AppFilter.vue";

export default {
  data() {
    return {
      title: "hello"
    }
  },
  components: {
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

.content{
  width: 1000px;
  min-height: 700px;
  background-color: #fff;
  margin: 0 auto;
  padding: 5rem 0;
}
</style>
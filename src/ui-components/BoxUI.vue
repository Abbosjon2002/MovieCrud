<template>
  <div class="box">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "BoxUI"
}
</script>

<style scoped>
.box {
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 0 10px 15px #00000030;
}
</style>
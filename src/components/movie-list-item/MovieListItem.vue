<template>
  <li class="list-group-item d-flex justify-content-between" :class="[{like: movie.like},{favourite: movie.favourite}]">
    <span class="list-group-item-label" @click="$emit('onToggle', {id: movie.id, prop: 'like' })">{{ movie.name }}</span>
    <input type="number" class="list-group-item-input" :value="movie.viewers">
    <div class="d-flex justify-content-center align-items-center">
      <button type="button" class="btn-cookies btn-sm" @click="$emit('onToggle', {id: movie.id, prop: 'favourite' })">
        <i class="fas fa-cookie"></i>
      </button>
      <button type="button" class="btn-trash btn-sm" @click="$emit('removeItem', movie.id)">
        <i class="fas fa-trash"></i>
      </button>
      <i class="fas fa-star star"></i>
    </div>
  </li>
</template>

<script>
export default {
  name: "MovieListItem",
  props: {
    movie: {
      type: Object,
      required: true
    }
  },
  methods: {
    onLike() {
      this.$emit('onLike', this.movie.id)
    },
    onFavourite() {
      this.$emit('onFavourite', this.movie.id)
    }
  }
}
</script>

<style scoped>
.list-group-item {
  padding: 15px 25px;
  border: none;
  border-bottom: 1px solid #00000020;
}

.list-group-item:last-child {
  border-bottom: none;
}

.list-group-item span {
  line-height: 35px;
  font-size: 20px;
  cursor: pointer;
  width: 50%;
}

.list-group-item input {
  line-height: 35px;
  font-size: 20px;
  text-align: center;
  border: none;
  outline: none;
}

.list-group-item button {
  width: 35px;
  height: 35px;
  margin: 3px;
  font-size: 17px;
  border: none;
  cursor: pointer;
}

.list-group-item .btn-cookies {
  color: #e09f0e;
}

.list-group-item .btn-trash {
  color: #e5383b;
}

.list-group-item .star {
  width: 35px;
  height: 35px;
  font-size: 16px;
  line-height: 35px;
  text-align: center;
  color: #ffd700;
  transition: .3s all;
  transform: translateX(30px);
  opacity: 0;
}

.list-group-item.like .star {
  transform: translateX(0);
  opacity: 1;
}

.list-group-item.favourite span, .list-group-item.favourite input {
  color: #e09f0e;
}
</style>
<template>
  <div class="cat-card">
    <img :src="src" alt="" class="cat-card__img">
  </div>
</template>

<script>
  export default {
    name: 'CatCard',

    props: {
      src: {
        type: String,
        required: true
      },

      heigth: {
        type: Number,
        required: true
      },

      width: {
        type: Number,
        required: true
      },
    }
  }
</script>

<style lang="scss" scoped>
  .cat-card {
    &__img {
      width: 100%;
      height: 200px;
      object-fit: cover;
    }
  }
</style>

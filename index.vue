<template lang="pug">
  .flip-card(:style="{ height, }" :class="{ turned, hover, }")
    .flip-card-inner
      .flip-card-front(ref="front")
        slot(name="front")
      .flip-card-back(ref="back")
        slot(name="back")
</template>

<script>
export default {
  name: 'vue-flip',
  props: {
    height: String,
    turned: Boolean,
    hover: Boolean,
  },
  watch: {
    height () {
      this.$refs.front.firstElementChild.style.height = this.height
      this.$refs.back.firstElementChild.style.height = this.height
    }
  }
}
</script>

<style lang="scss" scoped>
  .flip-card {
    background-color: transparent;
    perspective: 1000px;
  }

  .flip-card-inner {
    position: relative;
    width: 100%;
    height: 100%;
    text-align: center;
    transition: transform 0.6s;
    transform-style: preserve-3d;
  }

  .flip-card.turned,
  .flip-card.hover:hover {
    .flip-card-inner {
      transform: rotateY(180deg);
    }
  }

  .flip-card-front,
  .flip-card-back {
    position: absolute;
    width: 100%;
    height: 100%;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
  }


  .flip-card-back {
    transform: rotateY(180deg);
  }
</style>
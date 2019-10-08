<template>
  <transition :name="'slide-' + direction">
    <div v-show="visible" class="carousel-slide">
      <slot/>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'carousel-slide',
  data() {
    return {
      index: 0
    }
  },
  computed: {
    visible() {
      return this.index === this.$parent.index
    },
    direction() {
      return this.$parent.direction
    }
  }
}
</script>

<style scoped>
@keyframes slideRightIn {
  from { transform: translateX(100%) }
  to { transform: translateX(0) }
}
@keyframes slideRightOut {
  from { transform: translateX(0) }
  to { transform: translateX(-100%) }
}
.slide-right-enter-active {
  animation: slideRightIn .5s;
}
.slide-right-leave-active {
  animation: slideRightOut .5s;
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  width: 100%;
  height: 100%;
}
@keyframes slideLeftIn {
  from { transform: translateX(-100%) }
  to { transform: translateX(0) }
}
@keyframes slideLeftOut {
  from { transform: translateX(0) }
  to { transform: translateX(100%) }
}
.slide-left-enter-active {
  animation: slideLeftIn .5s;
}
.slide-left-leave-active {
  animation: slideLeftOut .5s;
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  width: 100%;
}

.carousel-slide {
  width: 100%;
  height: 100%;
}
</style>

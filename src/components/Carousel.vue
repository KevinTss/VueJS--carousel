<template>
  <div class="carousel">
    <slot/>
    <button class="nav previous" @click="previous"><<</button>
    <button class="nav next" @click="next">>></button>
    <div class="pagination">
      <button 
        v-for="n in slidesCount" 
        :key="n"
        class='nav-button'
        :class='{ active: n - 1 === index }'
        @click="goToElement(n - 1)"
        >
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'carousel',
  data() {
    return {
      index: 0,
      slides: this.$children,
      direction: null
    }
  },
  computed: {
    slidesCount() {
      return this.slides.length
    }
  },
  mounted() {
   this.slides = this.$children
   this.slides.forEach((slide, i) => {
     slide.index = i
   })
  },
  methods: {
    next() {
      this.index++
      if (this.index >= this.slidesCount) {
        this.index = 0
      }
      this.direction = 'right'
    },
    previous() {
      this.index--
      if (this.index < 0) {
        this.index = this.slidesCount - 1
      }
      this.direction = 'left'
    },
    goToElement(index) {
      this.direction = index > this.index ? 'right' : 'left'
      this.index = index
    }
  }
}
</script>

<style scoped>
.carousel {
  position: relative;
  width: 100%;
  overflow: hidden;
}
.nav {
  width: 65px;
  height: 65px;
  background-color: black;
  color: white;
  border: none;
  outline: none;
  font-size: 22px;
  position: absolute;
  top: 50%;
  margin-top: -32px;
}
.previous {
  left: 10px;
}
.next {
  right: 10px;
}
.pagination {
  position: absolute;
  bottom: 10px;
  left: 0;
  right: 0;
  text-align: center;
}
.nav-button {
  display: inline-block;
  width: 10px;
  height: 10px;
  border-radius: 100%;
  background-color: black;
  outline: none;
  border: 1px solid white;
  margin: 0 2px;
  cursor: pointer;
}
.nav-button.active {
  background-color: white;
}
</style>

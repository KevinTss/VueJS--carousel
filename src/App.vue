<template>
  <div id="app">
    <carousel>
      <carousel-slide v-for="n in slides" :key="n">
        <img :src="'https://picsum.photos/800/500?i=' + n">
      </carousel-slide>
    </carousel>
  </div>
</template>

<script>
import Carousel from './components/Carousel.vue'
import CarouselSlide from './components/CarouselSlide.vue'

export default {
  name: 'app',
  components: {
    Carousel,
    CarouselSlide
  },
  data() {
    return {
      slides: 5
    }
  }
}
</script>

<style>
body {
  padding: 0;
  margin: 0;
}
img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>

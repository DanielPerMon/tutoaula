<template>
  <div class="app">
    <carousel @next="next" @prev="prev">
      <carousel-slide
        v-for="(slide, index) in slides"
        :key="slide"
        :index="index"
        :visibleSlide="visibleSlide"
        :direction="direction"
        class="carousel-slider"
      >
        <img :src="slide" :alt="slide" />
      </carousel-slide>
    </carousel>
  </div>
</template>

<script>
import axios from "axios";
import Carousel from './components/Carousel.vue';
import CarouselSlide from './components/CarouselSlide.vue';

export default {
  name: "gif",
  data() {
    return {
      slides: [],
      visibleSlide: 0,
      direction: 'left'
    };
  },
  components: {
    Carousel: Carousel,
    CarouselSlide: CarouselSlide,
  },
  computed:{
      slidesLen(){
          return this.slides.length;
      }
  },
  methods: {
    async getGifs() {
      const resp = await axios.get(
        "https://api.giphy.com/v1/gifs/trending?api_key=yc0AnMlscuWWurEOjrMr5zsyBnEJEMdy&limit=25&rating=g"
      );
      this.gifs = resp.data;
      console.log(this.gifs);
      for (let i = 0; i < this.gifs.data.length; i++) {
        this.slides[i] = this.gifs.data[i].images.original.url;
      }
      console.log(this.aux);
    },
    next(){
          if(this.visibleSlide >= this.slidesLen-1){
              this.visibleSlide=0;
          }
          else{
              this.visibleSlide++;
          }
          this.direction="left"
      },
      prev(){
          if(this.visibleSlide <= 0){
              this.visibleSlide=this.slidesLen-1;
          }
          else{
              this.visibleSlide--;
          }
          this.direction="right"
      }
  },
  created() {
    this.getGifs();
  },
};
</script>

<style>
.app {
  display: flex;
  justify-content: center;
}

</style>

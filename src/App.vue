<template>
  <div class="d-flex align-items-center justify-content-center p-4">
    <div class="row m-0 justify-content-center align-items-center" style="height:100vh">
      <div class="col-sm-12 col-lg-6">
        <app-carousel
        @finished="userChoices"
        width='100%' 
        :slides="[
          {
            id:1,
            img:'https://i1.sndcdn.com/artworks-000165384395-rhrjdn-t500x500.jpg'
          },
          {
            id:2,
            img:'https://i1.sndcdn.com/artworks-000185743981-tuesoj-t500x500.jpg'
          },
          {
            id:3,
            img:'https://i1.sndcdn.com/artworks-000158708482-k160g1-t500x500.jpg'
          },
          {
            id:4,
            img:'https://i1.sndcdn.com/artworks-000062423439-lf7ll2-t500x500.jpg'
          },
          {
            id:5,
            img:'https://i1.sndcdn.com/artworks-000028787381-1vad7y-t500x500.jpg'
          },
          {
            id:6,
            img:'https://i1.sndcdn.com/artworks-000108468163-dp0b6y-t500x500.jpg'
          },
          {
            id:7,
            img:'https://i1.sndcdn.com/artworks-000064920701-xrez5z-t500x500.jpg'
          }
          ]"></app-carousel>
      </div>
    </div>
  </div>
</template>

<script>
import Carousel from './components/Carousel.vue'
export default {
  components:{
    appCarousel:Carousel
  },
  methods:{
    userChoices(data){
      console.log(data)
    }
  }
}
</script>

<style>

</style>
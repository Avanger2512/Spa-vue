<template>
  <div class="home">
    <div class="container">
      <h1 class="title">
        Some Description
      </h1>

    </div>
    <swiper :options="swiperOption">
      <!-- begin slide -->
      <swiper-slide v-for="index in 5"
        :key="index">
        <router-link to="/" target="_blank">
          <img src="https://picsum.photos/640/360" alt="photo">
        </router-link>
      </swiper-slide>
      <!-- end slide -->
      <div class="swiper-button-prev" slot="button-prev"></div>
      <div class="swiper-button-next" slot="button-next"></div>
    </swiper>
  </div>
</template>

<script>
import { swiper, swiperSlide } from 'vue-awesome-swiper'

export default {
  name: 'home',
  components: {
    swiper,
    swiperSlide
  },
  data() {
      return {
        swiperOption: {
          slidesPerView: 3,
          spaceBetween: 10,
          pagination: {
            el: '.swiper-pagination',
            clickable: true
          },
          navigation: {
            nextEl: '.swiper-button-next',
            prevEl: '.swiper-button-prev'
          },
          breakpoints: {
            640: {
              slidesPerView: 1
            }
          }
        }
      }
    }
}
</script>

<style lang="sass" >




</style>

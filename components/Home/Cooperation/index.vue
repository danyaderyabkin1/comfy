<script setup lang="ts">
const breakpoints = ref({
  1: {
    slidesPerView: 1.15,
    spaceBetween: 10
  },
  480: {
    slidesPerView: 1.75,
    spaceBetween: 10
  },

  768: {
    slidesPerView: 2,
    spaceBetween: 30
  },

  992: {
    slidesPerView: 3,
    spaceBetween: 30
  }
})
defineProps({
  grayBg: {
    type: Boolean,
    required: false
  }
})
const cooperationItems = ref([
  {
    id: 1,
    title: 'Своя фабрика',
    description: 'У нас полностью своё производство, построенное на новейших современных технологиях',
    icon: 'warehouse.svg'
  },
  {
    id: 2,
    title: 'Более 8 лет на рынке',
    description: 'Наша мебель получила множество положительных отзывов за время нашей работы',
    icon: 'review.svg'
  },
  {
    id: 3,
    title: 'Маркетплейсы',
    description: 'Наша продукция представлена на WB, Ozon, Яндекс.Маркет. Доступна быстрая и бесплатная доставка.',
    icon: 'delivery.svg'
  },
  {
    id: 4,
    title: 'Продуманная мебель',
    description: 'Удобству сборки нашей мебели мы отнесли особо внимание. Справиться сможет любой.',
    icon: 'check.svg'
  },
  {
    id: 5,
    title: 'Сертифицирована',
    description: 'Вся продукция прошла обязательную сертификацию. Материалы используются гипалергенные, натуральные.',
    icon: 'quality.svg'
  },
  {
    id: 6,
    title: 'Гарантия на изделия',
    description: '12 месяцев гарантии на нашу мебель',
    icon: 'certificate.svg'
  },
])

</script>

<template>
  <section :class="{gray: grayBg}" class="cooperation">
    <div class="container cooperation__container">
<!--      <h3>{{ title }}</h3>-->
<!--      <p class="cooperation__text">Мы ценим ваше время</p>-->
<!--      <img-->
<!--          class="cooperation__img" src="/assets/images/home/photo_2023-09-05-16.46.26-optimized.webp"-->
<!--          alt="cooperation">-->
      <h4>Почему <span class="primary--border">Comfy?</span></h4>
              <Swiper
                  class="swiper-why"
                  :modules="[SwiperAutoplay, SwiperNavigation]"
                  :slides-per-view="1.5"
                  :space-between="'20px'"
                  :pagination="{
                    enabled: true,
                    clickable: true
                    }"
                  :navigation="{
                  enabled: true,
                  nextEl: '.swiper-button-nextE',
                  prevEl: '.swiper-button-prevE',

                }"
                  :breakpoints="breakpoints"
              >
                <SwiperSlide v-for="(slide,index) in cooperationItems" :key="slide.id">
                  <div class="h-full flex items-start gap-4 bg-white rounded-2xl p-3">
                    <img class="w-8" :src="`/assets/images/home/${slide?.icon}`" alt="image">
                    <div>
                      <h5 class="font-semibold">{{slide?.title}}</h5>
                      <small>{{slide?.description}}</small>
                    </div>
                  </div>
                </SwiperSlide>


              </Swiper>
<!--              <div class="swiper-pagination"/>-->
      <ul class="cooperation__list">
        <li v-for="item in cooperationItems" :key="item.id">
          <div class="cooperation__image">
            <img :src="`/assets/images/home/${item.icon}`" alt="cooperation-icon">
          </div>
          <div class="cooperation__wrap">
            <h5>{{ item.title }}</h5>
            <p>{{ item.description }}</p>
          </div>
        </li>
      </ul>
    </div>
  </section>
</template>

<style scoped>

</style>
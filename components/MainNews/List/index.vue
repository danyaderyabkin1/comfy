<script setup lang="ts">
import { Swiper, SwiperSlide } from 'swiper/vue'
import { Autoplay, Pagination, Navigation } from 'swiper/modules'
import type { Swiper as SwiperType } from 'swiper'

const { fetchNews } = useNews()
const { data: news } = useAsyncData(() => fetchNews())

defineProps({
  bg: {
    type: Boolean,
    required: false
  }
})

const swiperInstance = ref<SwiperType | null>(null)

// Настройки слайдера
const swiperOptions = {
  modules: [Autoplay, Navigation],
  slidesPerView: 3,
  spaceBetween: 20,
  loop: true,
  autoplay: {
    delay: 5000,
    disableOnInteraction: false,
  },
  navigation: {
    nextEl: '.news-navigation-next',
    prevEl: '.news-navigation-prev',
  },
  watchSlidesProgress: true,
  breakpoints: {
    1: {
      slidesPerView: 1,
      spaceBetween: 10
    },
    480: {
      slidesPerView: 2,
      spaceBetween: 10
    },

    768: {
      slidesPerView: 3,
      spaceBetween: 30
    }
  }
}

const onSwiper = (swiper: SwiperType) => {
  swiperInstance.value = swiper
}

const nextSlide = () => {
  if (swiperInstance.value) {
    swiperInstance.value.slideNext()
  }
}

const prevSlide = () => {
  if (swiperInstance.value) {
    swiperInstance.value.slidePrev()
  }
}
</script>

<template>
  <section class="news">
    <div :class="{'bg-white': bg}" class="news__container">
      <NuxtLink to="news">
        <h3 class="title">Публикации</h3>
      </NuxtLink>

      <!-- Контейнер для навигации -->
      <div class="news-navigation">
        <button class="news-navigation-prev" @click="prevSlide">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
            <path d="M15 18L9 12L15 6" stroke="currentColor" stroke-width="2"/>
          </svg>
        </button>
        <button class="news-navigation-next" @click="nextSlide">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
            <path d="M9 18L15 12L9 6" stroke="currentColor" stroke-width="2"/>
          </svg>
        </button>
      </div>

      <div class="news-slider news__list">
        <Swiper
            v-bind="swiperOptions"
            @swiper="onSwiper"
            class="news-swiper"
        >
          <SwiperSlide
              v-for="(item, index) in news"
              :key="item?.id"
          >
            <MainNewsListItem
                :article="item"
            />
          </SwiperSlide>
        </Swiper>
      </div>
    </div>
  </section>
</template>

<style scoped lang="scss">
.swiper-slide {
  height: auto !important;
}

/* Стили для навигации */
.news-navigation {
  position: absolute;
  top: 50%;
  right: 0;
  display: flex;
  justify-content: space-between;
  width: 100%;
  gap: 10px;
  z-index: 10;
  margin-top: 2rem;
}

.news-navigation-prev,
.news-navigation-next {
  width: 40px;
  height: 40px;
  border: 1px solid #ccc;
  border-radius: 50%;
  background: white;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
}

.news-navigation-prev:hover,
.news-navigation-next:hover {
  background: #f5f5f5;
  border-color: #999;
}

/* Базовые стили для десктопной версии - теперь управляем opacity изображения */
:deep(.swiper-slide:not(.swiper-slide-next)) .news-item__image,
:deep(.swiper-slide:not(.swiper-slide-next)) .news-item__overlay {
  opacity: 0;
}

/* Для слайда с классом swiper-slide-next показываем изображение */
:deep(.swiper-slide-next) .news-item__image,
:deep(.swiper-slide-next) .news-item__overlay {
  opacity: 1;
}

/* Мобильная версия - все слайды с изображением */
@media (max-width: 768px) {
  :deep(.swiper-slide) .news-item__image,
  :deep(.swiper-slide) .news-item__overlay {
    opacity: 1;
  }
}

/* Для очень маленьких экранов */
@media (max-width: 480px) {
  :deep(.swiper-slide) .news-item__image {
    opacity: 1;
  }
}

/* Для планшетов (768px - 1024px) можно оставить десктопное поведение */
@media (min-width: 769px) and (max-width: 1024px) {
  :deep(.swiper-slide:not(.swiper-slide-next)) .news-item__image,
  :deep(.swiper-slide:not(.swiper-slide-next)) .news-item__overlay {
    opacity: 0;
  }

  :deep(.swiper-slide-next) .news-item__image,
  :deep(.swiper-slide-next) .news-item__overlay {
    opacity: 1;
  }
}
</style>
<script setup lang="ts">
const props = defineProps({
  article: {
    type: Object,
    required: true
  }
})

const date = computed(() => {
  if (!props.article) return null;

  // Разбиваем строку на части
  const [datePart] = props.article.active_after.split(' ');
  const [day, month, year] = datePart.split('.');

  // Создаем дату из полученных частей (месяц - 1, так как в JS месяцы 0-11)
  const date = new Date(year, month - 1, day);

  // Форматируем дату как "Июнь 13, 2025"
  const monthName = date.toLocaleString('ru-RU', { month: 'long' });
  // Делаем первую букву заглавной
  const capitalizedMonth = monthName.charAt(0).toUpperCase() + monthName.slice(1);

  return `${capitalizedMonth} ${day}, ${year}`;
});
</script>

<template>
  <li class="news-item">
    <!-- Абсолютно позиционированное изображение -->
    <img
        v-if="article?.preview_image"
        :src="article.preview_image"
        alt=""
        class="news-item__image"
    >

    <!-- Темный оверлей -->
    <div class="news-item__overlay"></div>

    <!-- Контент -->
    <div class="news-item__content">
      <div class="news__wrapper">
        <span class="position-absolute white">{{ date }}</span>
        <span class="news__dots flex align-top self-start leading-none absolute left-1/2 white">...</span>
        <NuxtLink class="news__blog white">Блог</NuxtLink>
      </div>
      <NuxtLink class="news__link white" :to="article?.url">{{article?.title}}</NuxtLink>
      <NuxtLink class="news__more text-[#707487] font-semibold white" to="/news">Подробнее</NuxtLink>
    </div>
  </li>
</template>

<style scoped>
.news-item {
  display: flex;
  flex-direction: column;
  gap: 10px;
  background-color: white;
  border-radius: 45px;
  position: relative;
  box-shadow: 0 2px 4px 0 #00000003;
  padding: 2rem;
  height: 100%;
  overflow: hidden; /* Чтобы изображение не выходило за границы */
}

/* Абсолютно позиционированное изображение */
.news-item__image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 45px;
  opacity: 0;
  transition: opacity 0.5s ease;
  z-index: 0;
}

/* Темный оверлей */
.news-item__overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: #00000050;
  border-radius: 45px;
  opacity: 0;
  transition: opacity 0.5s ease;
  z-index: 1;
  pointer-events: none;
}

/* Контент поверх изображения и оверлея */
.news-item__content {
  position: relative;
  z-index: 2;
  height: 100%;
  display: flex;
  flex-direction: column;
}

/* Базовые стили для текста (белый фон) */
.swiper-slide-next .news-item :deep(span.white),
.swiper-slide-next .news-item :deep(a.white) {
  color: #fff;
}

.news-item :deep(.white) {
  color: #5E0144;
}

.swiper-slide-next .news-item :deep(.news__link.white) {
  border-top: 1px dashed #fff;
  color: #fff;
}

.swiper-slide-next .news-item :deep(.news__more.white) {
  border-top: 1px dashed #fff;
  color: #fff;
}

.news-item :deep(.news__link.white) {
  border-top: 1px dashed #000;
  color: #000;
}

.news-item :deep(.news__more.white) {
  border-top: 1px dashed #000;
  color: #707487;
}

/* Стили для слайда с изображением */
:deep(.swiper-slide-next) .news-item__image,
:deep(.swiper-slide-next) .news-item__overlay {
  opacity: 1;
}

:deep(.swiper-slide-next) .news-item :deep(.white) {
  color: #fff;
}

:deep(.swiper-slide-next) .news-item :deep(.news__link.white),
:deep(.swiper-slide-next) .news-item :deep(.news__more.white) {
  border-top: 1px dashed #fff;
  color: #fff;
}

/* Мобильная версия - все слайды с изображением */
@media (max-width: 768px) {
  .news-item__image,
  .news-item__overlay {
    opacity: 1 !important;
  }

  .news-item :deep(span.white),
  .news-item :deep(a.white),
  .news-item :deep(.white) {
    color: #fff !important;
  }

  .news-item {
    background-color: transparent;
  }

  .news-item :deep(.news__link.white),
  .news-item :deep(.news__more.white) {
    border-top: 1px dashed #fff !important;
    color: #fff !important;
  }
}
</style>
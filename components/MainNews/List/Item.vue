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
  <li :class="{white: article?.preview_image}" :style="`background-image: url(${article?.preview_image})`">

<!--    <NuxtLink v-else :to="article?.url">-->
<!--      <img src="/assets/images/nophoto.jpg" alt="nophoto">-->
<!--    </NuxtLink>-->
    <div class="news__wrapper">
      <span :class="{white: article?.preview_image}"  class="position-absolute">{{ date }}</span>
      <span :class="{white: article?.preview_image}"  class="news__dots flex align-top self-start leading-none absolute left-1/2">...</span>
      <NuxtLink :class="{white: article?.preview_image}"  class="news__blog">Блог</NuxtLink>
    </div>
    <NuxtLink :class="{white: article?.preview_image}"  class="news__link" :to="article?.url">{{article?.title}}</NuxtLink>
    <NuxtLink :class="{white: article?.preview_image}" to="/news" class="news__more text-[#707487] font-semibold">Подробнее</NuxtLink>
<!--    <NuxtLink v-if="article?.preview_image" :to="article?.url">-->
<!--      <img-->
<!--          :src="article?.preview_image"-->
<!--          alt="article">-->
<!--    </NuxtLink>-->
  </li>
</template>

<style scoped>

</style>
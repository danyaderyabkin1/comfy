<script setup lang="ts">
const {fetchNews} = useNews()
const {data: news} = useAsyncData(() => fetchNews())
defineProps({
  bg: {
    type: Boolean,
    required: false
  }
})

</script>

<template>
  <section class="news">
    <div :class="{'bg-white': bg}" class="news__container">
      <NuxtLink to="news"><h3 class="title">Публикации</h3></NuxtLink>
      <ul class="news__list">
        <MainNewsListItem v-for="item in news" :key="item?.id" :article="item"/>
      </ul>
    </div>
  </section>
</template>

<style scoped>

</style>
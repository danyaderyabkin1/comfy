<script setup lang="ts">
const {fetchNews} = useNews()
const {data: news} = await useAsyncData(() => fetchNews())

const route = useRoute()
const config = useRuntimeConfig()
const canonicalUrl = `${config.public.siteUrl || 'https://otellica.ru'}${route.path}`

// Добавляем мета-теги и каноническую ссылку
useHead({
  link: [
    { rel: 'canonical', href: canonicalUrl }
  ]
})

useSeoMeta({
  title: 'Публикации Otellica',
  ogTitle: 'Публикации Otellica',
  description: 'Публикации Otellica',
  ogDescription: 'Публикации Otellica',
  ogImage: 'https://otellica.ru/assets/images/logo.webp',
})
</script>

<template>
  <main class="main">
    <section class="news">
      <div class="container news__container">
        <h3 class="title">Публикации</h3>
        <ul class="news__list">
          <MainNewsListItem v-for="item in news" :key="item?.id" :article="item"/>
        </ul>
      </div>
    </section>
  </main>
</template>

<style scoped>

</style>
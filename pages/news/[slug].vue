<script setup lang="ts">
const route = useRoute()
const cleanPath = route.path.startsWith('/') ? route.path.slice(1) : route.path
const {fetchArticle} = useArticle()
const {data: article} = await useAsyncData(() => fetchArticle(cleanPath))
const config = useRuntimeConfig()
const canonicalUrl = `${config.public.siteUrl || 'https://otellica.ru'}${route.path}`

// Добавляем мета-теги и каноническую ссылку
useHead({
  link: [
    { rel: 'canonical', href: canonicalUrl }
  ]
})

useSeoMeta({
  title: article.value?.meta_title,
  ogTitle: article.value?.meta_title,
  description: article.value?.meta_description,
  ogDescription: article.value?.meta_description,
  ogImage: 'https://otellica.ru/assets/images/logo.webp',
})
</script>

<template>
  <main class="main">
    <section class="article">
      <div class="container article__container">
        <UBreadcrumb
            class="mb-6"
            divider="/"
            :links="[{ label: 'Главная', to: '/' }, { label: 'Публикации', to: '/news' }, { label: article?.title }]"
        />
        <h1 class="title">{{ article?.title }}</h1>
        <div class="article__wrap">
          <!--          <a class="article__wrap-img" :href="currentArticle.yoast_head_json?.og_image[0]?.url" data-fancybox="gallery">-->
          <!--            <img-->
          <!--                :src="currentArticle.yoast_head_json?.og_image[0]?.url" :alt="currentArticle.title.rendered"-->
          <!--                draggable="false">-->
          <!--          </a>-->
          <div v-html="article?.content"/>
        </div>
      </div>
    </section>
  </main>
</template>

<style scoped>

</style>
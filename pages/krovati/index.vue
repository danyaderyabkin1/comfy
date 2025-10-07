<script setup lang="ts">
import {useCategoriesBySlug} from "~/composables/useCategoryBySlug";


const route = useRoute()
const cleanPath = route.path.startsWith('/') ? route.path.slice(1) : route.path
const {fetchCategories} = useCategoriesBySlug();
const {data: category} = await useAsyncData(() => fetchCategories(cleanPath))

const config = useRuntimeConfig()
const canonicalUrl = `${config.public.siteUrl || 'https://otellica.ru'}${route.path}`

// Добавляем мета-теги и каноническую ссылку
useHead({
  link: [
    { rel: 'canonical', href: canonicalUrl }
  ]
})

useSeoMeta({
  title: 'Текстиль для отелей и гостиниц - Otellica',
  ogTitle: 'Текстиль для отелей и гостиниц - Otellica',
  description: 'Любой текстиль для отелей и гостиниц, большой выбор различного текстиля. Комфорт за которым гости будут возвращаться снова.',
  ogDescription: 'Любой текстиль для отелей и гостиниц, большой выбор различного текстиля. Комфорт за которым гости будут возвращаться снова.',
  ogImage: 'https://otellica.ru/assets/images/logo.webp',
})

const cleanText = (html: string | null) => html.replace(/<[^>]*>/g, '')
</script>

<template>
  <main class="main">
    <MainBanner
        :image="category?.image"
        :title="cleanText(category?.preview_content)"
        :description="cleanText(category?.content)"
        :not-main-banner='true'/>
<!--    <TheCategory :title="category?.subTitle" :category-id="category?.id" :custom-grid="true"/>-->
<!--    <MainDescription title="Причины не экономить на текстиле" :list-items="descriptionItems"/>-->
    <!--    <HomeCooperation title="ПОЧЕМУ ВАМ БУДЕТ КОМФОРТНО С OTELLICA?" :gray-bg="false"/>-->
<!--    <MainForm/>-->
  </main>
</template>

<style scoped>

</style>
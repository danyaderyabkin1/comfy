<script setup lang="ts">
import {useCategoriesBySlug} from "~/composables/useCategoryBySlug";
import {usePostel} from "~/composables/constants/itemsTPostel";
import {usePad} from "~/composables/constants/itemsTPad";
import {useBlank} from "~/composables/constants/itemsTBlank";
import {useMat} from "~/composables/constants/itemsTMat";
import {useHat} from "~/composables/constants/itemsTHat";
import {useTow} from "~/composables/constants/itemsTTow";

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
  title: category.value?.meta_title,
  ogTitle: category.value?.meta_title,
  description: category.value?.meta_description,
  ogDescription: category.value?.meta_description,
  ogImage: 'https://otellica.ru/assets/images/logo.webp',
})

const cleanText = (html: string) => html.replace(/<[^>]*>/g, '')

const {itemsPostelEdge, itemsPostelChoice} = usePostel()
const {itemsPadEdge, itemsPadChoice} = usePad()
const {itemsBlankEdge, itemsBlankChoice} = useBlank()
const {itemsMatEdge, itemsMatChoice} = useMat()
const {itemsHatEdge, itemsHatChoice} = useHat()
const {itemsTowEdge, itemsTowChoice} = useTow()
</script>

<template>
  <main class="main">
    <MainBanner
        :title="cleanText(category?.preview_content)"
        :description="cleanText(category?.content)"
        :not-main-banner="true"
        :image="category?.image"/>
    <ProductsList
        :title="category?.title"
        :category-id="category?.id"
        :grid-four="true"
    />

    <MainEdge
        v-if="category?.meta_keywords === 'postel'"
        title="Преимущества"
        :grid-four="true"
        :items="itemsPostelEdge"
    />

    <MainEdge
        v-if="category?.meta_keywords === 'pad'"
        title="Преимущества"
        image="125f307b9d93307c0516660f69ab3098.webp"
        :grid-four="true"
        :items="itemsPadEdge"
    />

    <MainEdge
        v-if="category?.meta_keywords === 'blank'"
        title="Преимущества"
        image="125f307b9d93307c0516660f69ab3098.webp"
        :grid-four="false"
        :items="itemsBlankEdge"
    />

    <MainEdge
        v-if="category?.meta_keywords === 'mat'"
        title="Преимущества"
        image="125f307b9d93307c0516660f69ab3098.webp"
        :grid-four="false"
        :items="itemsMatEdge"
    />

    <MainEdge
        v-if="category?.meta_keywords === 'hat'"
        title="Преимущества"
        image="125f307b9d93307c0516660f69ab3098.webp"
        :grid-four="false"
        :items="itemsHatEdge"
    />

    <MainEdge
        v-if="category?.meta_keywords === 'tow'"
        title="Преимущества"
        image="125f307b9d93307c0516660f69ab3098.webp"
        :grid-four="false"
        :items="itemsTowEdge"
    />
    <TheOptForm/>

    <MainChoice
        v-if="category?.meta_keywords === 'postel'"
        title="<strong>ПРАВИЛЬНЫЙ ВЫБОР ПОСТЕЛЬНОГО БЕЛЬЯ</strong> ЭТО УДОБСТВО ВАШИХ ГОСТЕЙ"
        image="post-b-n2-1-_1_.webp"
        :reverse="true"
        :items="itemsPostelChoice"
    />
    <MainChoice
        v-if="category?.meta_keywords === 'pad'"
        title="<strong>ПРАВИЛЬНЫЙ ВЫБОР ПОДУШЕК</strong> ДЛЯ УДОБСТВА ВАШИХ ГОСТЕЙ"
        image="podushki-check.jpeg"
        :reverse="true"
        :items="itemsPadChoice"
    />
    <MainChoice
        v-if="category?.meta_keywords === 'blank'"
        title="<strong>ПРАВИЛЬНЫЙ ВЫБОР ОДЕЯЛ</strong> ДЛЯ УДОБСТВА ВАШИХ ГОСТЕЙ"
        image="young_beautiful_woman_in_blue_pajamas_sitting_on_bed_resting_on-scaled 1 (1).jpg"
        :reverse="true"
        :items="itemsBlankChoice"
    />
    <MainChoice
        v-if="category?.meta_keywords === 'mat'"
        title="<strong>ПРАВИЛЬНЫЙ ВЫБОР НАМАТРАСНИКОВ</strong> ДЛЯ УДОБСТВА ВАШИХ ГОСТЕЙ"
        image="young_beautiful_woman_blue_pajamas_sitting_bed_waking_up_stretching-scaled-_1_.webp"
        :reverse="true"
        :items="itemsMatChoice"
    />
    <MainChoice
        v-if="category?.meta_keywords === 'hat'"
        title="<strong>ПРАВИЛЬНЫЙ ВЫБОР Халатов</strong> ДЛЯ УДОБСТВА ВАШИХ ГОСТЕЙ"
        image="halaty-check.jpeg"
        :reverse="true"
        :items="itemsHatChoice"
    />
    <MainChoice
        v-if="category?.meta_keywords === 'tow'"
        title="<strong>ПРАВИЛЬНЫЙ ВЫБОР ПОЛОТЕНЕЦ</strong> ДЛЯ УДОБСТВА ВАШИХ ГОСТЕЙ"
        image="polotenca-check.jpeg"
        :reverse="true"
        :items="itemsTowChoice"
    />
    <MainForm/>

  </main>
</template>

<style scoped>

</style>
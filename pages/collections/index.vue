<script setup lang="ts">
import {useDescriptions} from "~/composables/constants/itemsDescription";
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
  title: 'Кейсы Otellica',
  ogTitle: 'Кейсы Otellica',
  description: 'Наши кейсы и опыт последних лет',
  ogDescription: 'Наши кейсы и опыт последних лет',
  ogImage: 'https://otellica.ru/assets/images/logo.webp',
})
const {descriptionItems} = useDescriptions()
</script>

<template>
  <main class="main">
    <section class="collections">
      <div class="container collections__container">
        <div class="collections__wrap">
          <h1>Наши кейсы и опыт последних лет</h1>
          <p>В последние годы мы успешно реализовали ряд проектов
            по оснащению гостиниц и отелей, предоставляя нашим клиентам
            высококачественные решения для создания
            комфортной и уютной атмосферы их гостей.</p>
          <div class="collections__border">
            <p>Эти проекты являются ярким примером нашего подхода
              к оснащению гостиниц и отелей.
            </p>
            <p>Мы стремимся не только удовлетворить потребности клиентов,
              но и создавать уникальные пространства,
              которые вдохновляют и дарят комфорт каждый день.</p>
            <p> Мы уверены, что наши решения помогут отелям и гостиницам
              привлечь больше гостей и повысить уровень их удовлетворенности.</p>
          </div>
        </div>
        <img src="/assets/images/collections/da0c9fbea7c5de7e3994126164397a94.jpg" alt="photo">
      </div>
    </section>
    <CollectionsList :category-id="13" :per-page="9"/>
    <MainDescription title="Преимущества, которые стали причиной успеха этих проектов" :list-items="descriptionItems"/>
    <section>
      <div class="container flex flex-col items-center">
        <p class="w-full md:flex md:w-2/5 primary--border text-center mb-3"></p>
        <h2 class="w-full md:flex md:w-2/5 text-center font-semibold">Выбирая нас, вы делаете шаг к созданию комфортного
          и
          привлекательного пространства для ваших гостей, что положительно скажется на их впечатлениях и,
          соответственно, на вашем бизнесе.</h2>
      </div>
    </section>
    <MainForm/>
  </main>


</template>


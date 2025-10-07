<script setup lang="ts">
useSeoMeta({
  title: 'Комплексное оснащение отелей и гостиниц: от мебели до текстиля',
  ogTitle: 'Комплексное оснащение отелей и гостиниц: от мебели до текстиля',
  description: 'Полностью оснащаем отели и гостиницы текстилем и мебелью. Предлагаем комплексные решения под ваши параметры. Оснащаем так же фитнес-клубы.',
  ogDescription: 'Полностью оснащаем отели и гостиницы текстилем и мебелью. Предлагаем комплексные решения под ваши параметры. Оснащаем так же фитнес-клубы.',
  ogImage: 'https://otellica.ru/assets/images/logo.webp',
})
const descriptionSecond = ref([
  '- Широкий выбор моделей в каталоге',
  '- Антивандальные ткани и экологичные материалы',
  '- Вся продукция сертифицированна',
])

const itemsClients = ref([
  {
    id: 1,
    img: 'big-logo-400x401.webp',
    link: 'https://malamut-land.ru/'
  },
  {
    id: 2,
    img: '6568454.webp',
    link: 'https://berejkihall.ru/'
  },
  {
    id: 3,
    img: 'hMw1vPZugEFRQVErdYn7RQursDW6tIJe6cemmZairdPPKvbOpQB0GceuF1avpxPClcf_6NntlnsgFQls8UVbce0v.webp',
    link: 'https://vk.com/ax_alta'
  },
  {
    id: 4,
    img: 'logo.svg',
    link: 'https://imera.ru/'
  },
  {
    id: 5,
    img: 'logo_utes.svg',
    link: 'https://uteshotel.com/aktsii/'
  },
  {
    id: 6,
    img: '_logo_vector_2_RGB_b.svg',
    link: 'https://chigish.ru/'
  }
])

</script>

<template>


  <main class="main">

    <MainBanner
        image="/assets/images/banners/c3b32af52d8d233c4681339b30392e8b97e07a03.webp"
        title="Детская мебель из натуральных материалов"
        description=""
        :second-description="descriptionSecond"
        :contrast="false"
        :bg-color="true"
        :not-main-banner="false"/>
    <HomeCooperation/>
    <HomeInv/>
<!--    <HomeServices-->
<!--        :title='`Оснащение <span class="primary&#45;&#45;border">отелей и гостиниц</span>`'-->
<!--        :left-wrap="{title: 'Мебель', link: '/mebel', image: 'l1-1-768x513-optimized.webp'}"-->
<!--        :right-wrap="{title: 'Текстиль', link: '/krovati', image: 'chambermaid-making-bed-in-hotel-room-768x513-optimized.webp'}"-->
<!--    />-->
    <!--    <HomeServices-->
    <!--        :title='`Оснащение <span class="primary&#45;&#45;border">фитнес-клубов</span>`'-->
    <!--        :left-wrap="{title: 'ОБОРУДОВАНИЕ', link: '/oborudovaniye-dlya-fintes-klubov', image: 'tren3-768x513-optimized.webp'}"-->
    <!--        :right-wrap="{title: 'ТЕКСТИЛЬ', link: '/osnashchenie-fitnes-klubov', image: 'meb-tek2-768x513-optimized.webp'}"-->
    <!--    />-->
<!--    <HomePay/>-->
<!--    <HomeClients title="Наши партнеры" :items="itemsClients"/>-->
<!--    <ClientOnly>-->
<!--      <MainReviews/>-->
<!--    </ClientOnly>-->
    <!--    <HomeQuiz/>-->

    <!--    <HomeServices-->
    <!--        title="ОСНАЩАЕМ РЕСТОРАНЫ"-->
    <!--        :left-wrap="{title: 'МЕБЕЛЬ', link: '/osnashchenie-restoranov-i-kafe', image: 'rest4-768x512-optimized.webp'}"-->
    <!--        :right-wrap="{title: 'ТЕКСТИЛЬ', link: '/osnashchenie-restoranov-i-kafe', image: 'rest-trxt3-768x512-optimized.webp'}"-->
    <!--    />-->

    <HomeKomfort/>
    <MainNewsList/>
    <HomeGallery/>
<!--    <MainForm/>-->
  </main>

</template>

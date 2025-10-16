<script setup lang="ts">
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
  title: 'О нашей компании ',
  ogTitle: 'О нашей компании ',
  description: 'История компании началась с желания создать кровати',
  ogDescription: 'История компании началась с желания создать кровати',
  ogImage: 'https://otellica.ru/assets/images/logo.webp',
})
// const items = [
//   '/assets/images/about/dec_237670_page-0001-1-optimized.webp',
//   '/assets/images/about/00208__page-0001-optimized.webp',
// ]
// const itemsThx = [
//   '/assets/images/about/photo_2025-02-27_10-42-39.jpg',
//   '/assets/images/about/photo_2025-02-27_10-42-44.jpg',
//   '/assets/images/about/IMG-20250313-WA01062.jpg',
//   '/assets/images/about/bl-ot-4.jpg',
//   '/assets/images/about/th1.webp',
// ]
// const modal = ref(false)
const descriptionSecond = ref([
  '- Широкий выбор моделей в каталоге',
  '- Антивандальные ткани и экологичные материалы',
  '- Вся продукция сертифицированна',
])
// const {fetchCategories} = useCategories();
// const {data} = useAsyncData(() => fetchCategories(), {immediate: true});

</script>

<template>
  <main class="main">
    <MainBanner
        :image="[
          '/assets/images/banners/c3b32af52d8d233c4681339b30392e8b97e07a03.jpg',
          '/assets/images/banners/7fd4a21d9940dbe7640d0d68755fcb3e3b4cd456.jpg',
          '/assets/images/banners/c3b32af52d8d233c4681339b30392e8b97e07a03.jpg',
         '/assets/images/banners/7fd4a21d9940dbe7640d0d68755fcb3e3b4cd456.jpg',
         '/assets/images/banners/c3b32af52d8d233c4681339b30392e8b97e07a03.jpg',
        ]"
        title="Детская мебель из натуральных материалов"
        description=""
        :second-description="descriptionSecond"
        :contrast="false"
        :bg-color="true"
        :not-main-banner="false"/>
    <HomeCooperation/>
    <HomeInv/>
    <HomeKomfort/>
    <MainNewsList/>
    <HomeGallery/>
<!--    <section id="about" class="about">-->
<!--      <div class="container about__container">-->
<!--        <h1>О компании</h1>-->
<!--        <div class="about__wrap">-->
<!--          <img src="/assets/images/about/PHOT4851-683x1024-optimized.webp" alt="SEO">-->
<!--          <div>-->
<!--            <p>Здравствуйте!</p>-->
<!--            <p class="mb-2">-->
<!--              Меня зовут Александр Мальцев, и я – директор компании “Отеллика”.</p>-->
<!--            <p class="mb-2">Наша компания специализируется на комплексном оснащении гостиничного бизнеса-->
<!--              высококачественными-->
<!--              текстильными-->
<!--              изделиями и корпусной мебелью.</p>-->
<!--            <p class="mb-2">Более четырех лет опыта работы в данной сфере, включая работу в крупной известной-->
<!--              компании-лидере на рынке, позволили мне принять решение начать свой собственный путь с целью-->
<!--              предоставления-->
<!--              высококачественного сервиса нашим партнерам.-->
<!--            </p>-->
<!--            <p class="mb-2">Наша компания – молодая и амбициозная. Ответственность и забота о клиентах – наши главные-->
<!--              принципы. Мы гарантируем, что все потребности и желания наших клиентов будут восприняты как свои личные, и-->
<!--              мы-->
<!--              готовы предоставить индивидуальный подход к каждому заказчику.-->
<!--            </p>-->
<!--            <p class="mb-2">Мы убеждены, что важнее всего для нас – это наше имя и репутация в узкоспециализированном-->
<!--              рынке.-->
<!--              Несмотря на молодость, наш подход к работе превосходит ожидания, благодаря многолетнему опыту и-->
<!--              экспертности-->
<!--              в-->
<!--              данной области.-->
<!--            </p>-->
<!--            <p class="mb-2">Станем вашими надежными партнерами в развитии вашего бизнеса. Доверьтесь нам, и вы не-->
<!--              пожалеете!</p>-->
<!--          </div>-->
<!--        </div>-->
<!--      </div>-->
<!--    </section>-->
<!--    <HomeAdvantages/>-->
<!--    <AboutSuggestion-->
<!--        :key="1"-->
<!--        :id-form="24"-->
<!--        :title='`Если у Вас есть предложения, пожелания или замечания напишите нам об этом и руководство компании <span class="primary&#45;&#45;border flex w-fit mx-auto">лично займется Вашим вопросом</span>`'/>-->

<!--    <section id="sert" class="certificate">-->
<!--      <div class="container">-->
<!--        <h3 class="title primary&#45;&#45;border w-fit mx-auto">Сертификаты</h3>-->
<!--        <div class="certificate__wrap ">-->
<!--          <a v-for="(item, index) in items" :key="index" :href="item" data-fancybox="gallery">-->
<!--                  <img :src="item" class="w-full" draggable="false" alt="certificate">-->
<!--              </a>-->
<!--&lt;!&ndash;          <UCarousel&ndash;&gt;-->
<!--&lt;!&ndash;              :items="items"&ndash;&gt;-->
<!--&lt;!&ndash;              :ui="{&ndash;&gt;-->
<!--&lt;!&ndash;          item: 'basis-full',&ndash;&gt;-->
<!--&lt;!&ndash;          container: 'rounded-lg'&ndash;&gt;-->
<!--&lt;!&ndash;        }"&ndash;&gt;-->
<!--&lt;!&ndash;              arrows&ndash;&gt;-->
<!--&lt;!&ndash;              class="w-64 mx-auto"&ndash;&gt;-->
<!--&lt;!&ndash;          >&ndash;&gt;-->
<!--&lt;!&ndash;            <template #default="{ item }">&ndash;&gt;-->
<!--&lt;!&ndash;              <a :href="item" data-fancybox="gallery">&ndash;&gt;-->
<!--&lt;!&ndash;                <img :src="item" class="w-full" draggable="false">&ndash;&gt;-->
<!--&lt;!&ndash;              </a>&ndash;&gt;-->
<!--&lt;!&ndash;            </template>&ndash;&gt;-->
<!--&lt;!&ndash;            <template #prev="{ onClick, disabled }">&ndash;&gt;-->
<!--&lt;!&ndash;              <button :disabled="disabled" @click="onClick">&ndash;&gt;-->
<!--&lt;!&ndash;                &#8249;&ndash;&gt;-->
<!--&lt;!&ndash;              </button>&ndash;&gt;-->
<!--&lt;!&ndash;            </template>&ndash;&gt;-->

<!--&lt;!&ndash;            <template #next="{ onClick, disabled }">&ndash;&gt;-->
<!--&lt;!&ndash;              <button :disabled="disabled" @click="onClick">&ndash;&gt;-->
<!--&lt;!&ndash;                &#8250;&ndash;&gt;-->
<!--&lt;!&ndash;              </button>&ndash;&gt;-->
<!--&lt;!&ndash;            </template>&ndash;&gt;-->
<!--&lt;!&ndash;          </UCarousel>&ndash;&gt;-->
<!--        </div>-->
<!--      </div>-->
<!--    </section>-->

<!--    <section class="control">-->
<!--      <div class="container control__container">-->
<!--        <h2 class="title"><span class="primary&#45;&#45;border flex w-fit mx-auto">Контроль процессов</span> от входящего сырья до конечного продукта!</h2>-->
<!--        <ul class="control__list">-->
<!--          <AboutControl/>-->
<!--        </ul>-->
<!--      </div>-->
<!--    </section>-->

<!--    <section id="thank" class="certificate">-->
<!--      <div class="container">-->
<!--        <h3 class="title primary&#45;&#45;border w-fit mx-auto">Благодарности</h3>-->
<!--        <div class="certificate__wrap">-->
<!--          <a v-for="(item, index) in itemsThx" :key="index" :href="item" data-fancybox="gallery">-->
<!--            <img :src="item" class="w-full" draggable="false" alt="image">-->
<!--          </a>-->
<!--        </div>-->
<!--      </div>-->
<!--    </section>-->

<!--    <section id="delivery" class="delivery">-->
<!--      <div class="container delivery__container">-->
<!--        <h3 class="title primary&#45;&#45;border w-fit mx-auto">Способы доствки</h3>-->
<!--        <p class="text-center w-full md:w-2/3 xl:w-1/3  mx-auto">Мы можем осуществить доставку Вашего груза по всей территории России и СНГ удобным для Вас способом</p>-->
<!--        <div class="delivery__wrap">-->
<!--          <ul class="delivery__list">-->
<!--            <li>-->
<!--              <img src="/assets/images/about/Mask-group-5-768x963-optimized.webp" alt="delivery-icon">-->
<!--              <h4>ТРАНСПОРТНАЯ КОМПАНИЯ</h4>-->
<!--              <p>Персональный менеджер поможет рассчитать вес и объем для транспортировки вашего груза и подберет для-->
<!--                вас оптимальную транспортную компанию</p>-->
<!--            </li>-->
<!--            <li>-->
<!--              <img src="/assets/images/about/photo_2023-10-04_13-03-48-3-1-768x691-optimized.webp" alt="delivery-icon">-->
<!--              <h4>ДОСТАВКА СИЛАМИ КОМПАНИИ «OTELLICA»</h4>-->
<!--              <p>Вы ни о чем не думаете, все хлопоты на наших плечах</p>-->
<!--            </li>-->

<!--          </ul>-->
<!--          <img src="/assets/images/about/aboutCar.webp" alt="delivery">-->
<!--          <ul class="delivery__list">-->
<!--            <li>-->
<!--              <img src="/assets/images/about/photo_2023-10-04_13-03-48-2-768x768-optimized.webp" alt="delivery-icon">-->
<!--              <h4>САМОВЫВОЗ СО СКЛАДА</h4>-->
<!--              <p>Вы можете самостоятельно забрать ваш заказ с нашего склада или производства</p>-->
<!--            </li>-->
<!--            <li>-->
<!--              <img-->
<!--                  src="/assets/images/about/photo_2023-10-04_13-03-48_4-transformed-1-optimized.webp"-->
<!--                  alt="delivery-icon">-->
<!--              <h4>БЕСПЛАТНАЯ ДОСТАВКА ДО ТЕРМИНАЛА-->
<!--              </h4>-->
<!--              <p>Без дополнительных затрат бесплатно доставим ваш заказ до терминала транспортной компании в нашем-->
<!--                регионе-->
<!--              </p>-->
<!--            </li>-->
<!--          </ul>-->
<!--        </div>-->
<!--      </div>-->
<!--    </section>-->
<!--    <AboutSuggestionTwo-->
<!--        :key="21"-->
<!--        :id-form="39"-->
<!--        :bg-color="true"-->
<!--        title="ЧТОБЫ ЗАПРОСИТЬ ОПТОВЫЕ ЦЕНЫ, ЗАПОЛНИТЕ ФОРМУ НИЖЕ"/>-->
<!--    <MainForm/>-->


  </main>


</template>


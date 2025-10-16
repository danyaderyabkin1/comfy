<script setup lang="ts">
useSeoMeta({
  title: 'Комплексное оснащение отелей и гостиниц: от мебели до текстиля',
  ogTitle: 'Комплексное оснащение отелей и гостиниц: от мебели до текстиля',
  description: 'Полностью оснащаем отели и гостиницы текстилем и мебелью. Предлагаем комплексные решения под ваши параметры. Оснащаем так же фитнес-клубов.',
  ogDescription: 'Полностью оснащаем отели и гостиницы текстилем и мебелью. Предлагаем комплексные решения под ваши параметры. Оснащаем так же фитнес-клубов.',
  ogImage: 'https://otellica.ru/assets/images/logo.webp',
})

const descriptionSecond = ref([
  '- Широкий выбор моделей в каталоге',
  '- Антивандальные ткани и экологичные материалы',
  '- Вся продукция сертифицированна',
])

// Состояние активного таба
const activeTab = ref('sales')

// Функция для переключения табов
const setActiveTab = (tab: string) => {
  activeTab.value = tab
}
</script>

<template>
  <main class="main bg-[#EFF0F2]">
    <MainBanner
        :image="[
          '/assets/images/banners/7fd4a21d9940dbe7640d0d68755fcb3e3b4cd456.jpg',
          '/assets/images/banners/c3b32af52d8d233c4681339b30392e8b97e07a03.jpg',
          '/assets/images/banners/7fd4a21d9940dbe7640d0d68755fcb3e3b4cd456.jpg',
          '/assets/images/banners/c3b32af52d8d233c4681339b30392e8b97e07a03.jpg',
         '/assets/images/banners/7fd4a21d9940dbe7640d0d68755fcb3e3b4cd456.jpg',
        ]"
        title="Закажите детскую безопасную мебель из качественных материалов"
        description=""
        :second-description="descriptionSecond"
        :contrast="false"
        :bg-color="true"
        :not-main-banner="false"/>

    <!-- Табы -->
    <section class="container mx-auto py-8">
      <div class="flex justify-center">
        <div class="flex gap-12 rounded-lg p-1">
          <button
              class="px-6 py-3 rounded-md transition-all duration-300"
              :class="activeTab === 'sales' ? 'btn btn-primary' : 'btn btn-white'"
              @click="setActiveTab('sales')"
          >
            Акции месяца
          </button>
          <button
              class="px-6 py-3 rounded-md transition-all duration-300"
              :class="activeTab === 'hits' ? 'btn btn-primary' : 'btn btn-white'"
              @click="setActiveTab('hits')"
          >
            Хиты продаж
          </button>
        </div>
      </div>

      <!-- Контент табов -->
      <div class="tab-content">
        <div v-show="activeTab === 'sales'">
          <ProductsList
              :category-id="499"
              :grid-four="false"
          />
        </div>
        <div v-show="activeTab === 'hits'">
          <ProductsList
              :category-id="501"
              :grid-four="false"
          />
        </div>
      </div>
    </section>

    <HomeCooperation/>

    <MainSwiperBanner/>


    <section class="py-12 bg-white  md:rounded-t-[60px]">
      <div class=" flex  title w-fit mx-auto mb-4">Отзывы&nbsp;о&nbsp;

        <h3 class="title primary--border"> нас</h3>

      </div>
      <div class="max-w-2xl p-2 mx-auto">
        <div style="width:100%;height:800px;overflow:hidden;position:relative;">
          <iframe style="width:100%;height:100%;border:1px solid #e6e6e6;border-radius:8px;box-sizing:border-box"
                  src="https://yandex.ru/maps-reviews-widget/70565141209?comments"></iframe>
          <a href="https://yandex.ru/maps/org/comfy_meb/70565141209/" target="_blank"
             style="box-sizing:border-box;text-decoration:none;color:#b3b3b3;font-size:10px;font-family:YS Text,sans-serif;padding:0 20px;position:absolute;bottom:8px;width:100%;text-align:center;left:0;overflow:hidden;text-overflow:ellipsis;display:block;max-height:14px;white-space:nowrap;padding:0 16px;box-sizing:border-box">Comfy-meb
            на карте Родников — Яндекс Карты</a></div>
      </div>
    </section>
  </main>
</template>

<style scoped>
.tab-content {
  transition: all 0.3s ease-in-out;
}

/* Плавная анимация переключения табов */
.tab-content > div {
  animation: fadeIn 0.3s ease-in-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
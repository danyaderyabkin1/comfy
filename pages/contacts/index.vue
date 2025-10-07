<script setup lang="ts">
</script>

<template>
  <main class="main">
    <section id="contacts" class="contacts">
      <h1 class="page-title mb-4">Контактная информация</h1>
      <UBreadcrumb
            class="mb-8 font-light text-gray-300 flex justify-center custom-breadcrumb"
            divider="-"
            :ui="{
        label: 'text-gray-500 font-light',
        separator: 'text-gray-300',
        separatorIcon: 'text-gray-500',
        list: 'text-gray-500',
        link: 'text-gray-300'
    }"
          :links="[{ label: 'Comfy', to: '/' }, {label: 'Контакты'}]"
      />

      <div class="container contacts__container max-w-7xl">

        <div>
          <TheModalFormOpt title="Обратная связь"/>
        </div>
        <div class="flex flex-col gap-10 text-xl">

          <div class="contact-item">
            <ul class="flex gap-5">
              <li>
                <a href="https://www.ozon.ru/brand/comfy-meb-100098308/?__rr=1" target="_blank">
                  <img class="w-10 rounded-full" src="/public/assets/images/about/c4e9bf55d8134a9f8e0a78968a5fb896747ea0d4.png" alt="ozon">
                </a>
              </li>
              <li>
                <a href="https://www.wildberries.ru/brands/comfy-meb" target="_blank">
                  <img class="w-10 rounded-full" src="/public/assets/images/about/2420fad29c780fcb5f42588d671df7c8da6ead15.png" alt="wb">
                </a>
              </li>
              <li>
                <a href="https://market.yandex.ru/business--comfy-meb/41471413" target="_blank">
                  <img class="w-10 rounded-full" src="/public/assets/images/about/b11d28bb16248ea516aa407ee955807d1f67e558.png" alt="market">
                </a>
              </li>
              <li>
                <a href="https://megamarket.ru/catalog/?q=comfy-meb&suggestionType=constructor" target="_blank">
                  <img class="w-10 rounded-full" src="/public/assets/images/about/1ddc6ce957049ccc5ac3c871f64fee742954df2d.png" alt="sber">

                </a>
              </li>
            </ul>
          </div>
          
            <div class="contact-item">
              <div class="contact-label primary--border w-fit text-2xl">Эл. почта:</div>
              <div class="contact-value">
                <a href="mailto:info@comfy-meb.ru" class="contact-link">info@comfy-meb.ru</a>
              </div>
            </div>

            <div class="contact-item text-xl">
              <div class="contact-label primary--border w-fit text-2xl">Адрес:</div>
              <div class="contact-value font-semibold">
                Ивановская область, г. Родники, ул. Трудовая, д. 16
              </div>
            </div>

            <div class="contact-item">
              <div class="contact-label primary--border w-fit text-2xl">Телефоны:</div>
              <div class="contact-value">
                <div class="phone-number font-semibold text-2xl">
                  <a href="tel:+79158251758" class="contact-link">+7 915 825 17 58</a>
                </div>
                <div class="phone-number font-semibold text-xl">
                  <a href="tel:+79115119990" class="contact-link">+7 911 511-99-90</a>
                </div>
              </div>
          </div>
<!--          <ul class="contacts__list">-->
<!--            <li>-->
<!--              <img src="/public/assets/images/about/SVGRepo_iconCarrier.svg" alt="phone-icon">-->
<!--              <div>-->
<!--                <p>-->
<!--                  <a class="contacts__link" href="tel:+7 (962) 169-05-51">+7 (962) 169-05-51 </a>-->
<!--                  <small class="block text-gray-500 mb-2.5">Бесплатно по России</small>-->
<!--                </p>-->
<!--                <p>-->
<!--                  <a class="contacts__link" href="tel:+7 (911) 511-99-90 ">+7 (911) 511-99-90 </a>-->
<!--                </p>-->
<!--              </div>-->
<!--            </li>-->
<!--            <li>-->
<!--              <img class="contacts__img" src="/public/assets/images/about/SVGRepo_iconCarrie.svg" alt="mail-icon">-->
<!--              <div>-->
<!--                <p>-->
<!--                  <a class="contacts__link" href="mailto:info@comfy-meb.ru">info@comfy-meb.ru</a>-->
<!--                </p>-->
<!--                <small class="block text-gray-500"> E-mail</small>-->
<!--              </div>-->

<!--            </li>-->
<!--          </ul>-->
        </div>
      </div>
      <iframe
          class="mt-8"
          src="https://yandex.ru/map-widget/v1/?from=api-maps&ll=41.758639%2C57.097557&mode=search&oid=70565141209&ol=biz&origin=jsapi_2_1_79&z=16.43" width="100%" height="404"
          frameborder="0"/>
<!--      <UModal v-model="modal" :ui="{ width: 'sm:max-w-3xl', container: 'items-center'}" class="modal w-full">-->
<!--        <UButton-->
<!--            color="gray"-->
<!--            variant="ghost" icon="i-heroicons-x-mark-20-solid" class="-my-1 modal__close"-->
<!--            @click.prevent="modal = false"/>-->
<!--        <div class="container">-->
<!--          <h4 class="title mb-6">Реквизиты</h4>-->
<!--          <div class="max-w-2xl mx-auto font-medium">-->
<!--            <p class="mb-3">Полное наименование: Общество с ограниченной ответственностью «ОТЕЛИКА»</p>-->
<!--            <p class="mb-3">Краткое наименование: ООО «ОТЕЛИКА»</p>-->
<!--            <p class="mb-3">Адрес электронной почты: otelicaiv@yandex.ru-->
<!--            </p>-->
<!--            <p class="mb-3">Контактный телефон: 8 (4932) 244 301-->
<!--            </p>-->
<!--            <p class="mb-3">ИНН / КПП: 3700010049/370001001-->
<!--            </p>-->
<!--            <p class="mb-3">ОГРН: 1233700008057-->
<!--            </p>-->
<!--            <p class="mb-3">Руководитель (должность, ФИО): Директор Мальцев Александр Валерьевич-->
<!--            </p>-->
<!--            <p class="mb-3">Главный бухгалтер: Мальцев Александр Валерьевич-->
<!--            </p>-->
<!--            <p class="mb-3">Наименование банка: Ивановское отделение №8639 ПАО Сбербанк-->
<!--            </p>-->
<!--            <p class="mb-3">БИК: 042406608-->
<!--            </p>-->
<!--            <p class="mb-3">Корреспондентский счет: 30101810000000000608-->
<!--            </p>-->
<!--            <p class="mb-3">Расчетный счет: 40702810517000050943-->
<!--            </p>-->
<!--          </div>-->
<!--        </div>-->
<!--      </UModal>-->
    </section>

  </main>
</template>
<style>
.custom-breadcrumb .text-muted,
.custom-breadcrumb .text-primary,
.custom-breadcrumb span:not([class]) {
  color: #6B7280 !important; /* gray-300 */
}
</style>
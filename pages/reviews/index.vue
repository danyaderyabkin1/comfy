<script setup lang="ts">
</script>

<template>
  <main class="main">
    <section class="description">
      <h1 class="page-title mb-4">Отзывы о нас</h1>
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
          :links="[{ label: 'Comfy', to: '/' }, {label: 'Отзывы'}]"
      />
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

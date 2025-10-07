<script setup lang="ts">
defineProps({
  title: {
    type: String,
    required: true
  },
  description: {
    type: String,
    required: true
  },
  secondDescription: {
    type: Array,
    required: false
  },
  image: {
    type: String,
    required: false
  },
  mobileImage: {
    type: String,
    required: false
  },
  contrast: {
    type: Boolean,
    required: false,
    default: true
  },
  bgColor: {
    type: Boolean,
    required: false,
  },
  notMainBanner: {
    type: Boolean,
    required: true,
    default: true
  }
})
const isOpen = ref(false)
</script>

<template>
  <section :class="{gray: bgColor}" class="hero">
    <div class="container">
      <picture v-if="image">
        <source media="(max-width:650px)" :srcset="mobileImage ?? image">
        <img :src="image" alt="connect-image">
      </picture>
      <div class="hero__container">
        <div :class="{contrast: contrast}" class="hero__wrapper">
          <h1 class="hero__title" :class="{'title--main': !notMainBanner}">{{ title }}</h1>
          <div v-if="notMainBanner" class="hero__separator my-2"></div>
          <p>{{ description }}</p>
          <ul v-if="secondDescription">
            <li v-for="(item, i) in  secondDescription" :key="i">{{ item }}</li>
          </ul>
        </div>

        <div class="hero__wrap-btn">
          <button class="btn btn-primary hero__btn" type="button" @click="isOpen = true">Оставить заявку</button>
          <div class="hero__contacts">
            <div class="hero__contacts-wrapper">
              <a
                  class="tg"
                  href="https://t.me/+79621690551"
                  target="_blank">
                <UIcon name="uil:telegram" class="size-9"/>
              </a>
              <a
                  class="what"
                  href="https://api.whatsapp.com/send/?phone=%2B79621690551&text&type=phone_number&app_absent=0"
                  target="_blank">
                <UIcon name="i-mingcute-whatsapp-fill" class="size-9"/>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>


    <MainModal v-model="isOpen"/>
  </section>
</template>

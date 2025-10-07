<script setup lang="ts">
defineProps({
  title: {
    type: String,
    required: true
  },
  listItems: {
    type: Array,
    required: true
  }
})

</script>

<template>
  <section class="description">
    <div class="container description__container">
      <h2 class="title mb-8 md:mb-16">{{ title }}</h2>
      <ul class="description__list">
        <li class="description__item" v-for="item in listItems" :key="item?.id">
          <div class="description__item-icon">
            <img :src="`/assets/images/description/${item.image}`" alt="icon">
          </div>
          <div>
            <h3>{{ item?.title }}</h3>
            <p>{{ item?.description }}</p>
          </div>
        </li>
      </ul>
    </div>
  </section>
</template>

<style scoped>

</style>
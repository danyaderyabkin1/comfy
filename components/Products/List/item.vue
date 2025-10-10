<script setup lang="ts">
const token = useCookie('_token')
const props = defineProps({
  product: {
    type: Object,
    required: true
  }
})
const emit = defineEmits(['openModal', 'addToCart'])

const cleanText = (html:string) => html.replace(/<[^>]*>/g, '')
const sendToCart = ref({
  items: [{
    domain: 'b.hoteltex.online',
    productId: props.product?.id,
    skuId: props.product?.sku[0]?.id,
    quantity: 1
  }]
})
const {fetchCart} = useCart()
const {fetchAddToCart} = useAddToCart()
const addToCart = async () => {
  if (!token.value) {
    // Обработка случая, когда пользователь не авторизован
    return;
  }

  try {
    await fetchAddToCart(token.value, sendToCart.value);
    emit('addToCart', 'Товар добавлен в заказ!', 'neutral');
    // Не нужно повторно вызывать fetchCart, так как он уже вызывается в fetchAddToCart
  } catch (error) {
    console.error('Failed to add to cart:', error);
    emit('addToCart', 'Произошла ошибка!', 'warning');
  }
};
</script>

<template>
  <li itemscope itemprop="itemListElement" itemtype="http://schema.org/Product">
<!--    <pre>{{product}}</pre>-->
    <NuxtLink v-if="product?.preview_image" :title="cleanText(product?.title)" :to="`${product?.url}`">
      <img :src="product?.preview_image" loading="lazy" alt="product-image" itemprop="image">
    </NuxtLink>
    <NuxtLink v-else :title="cleanText(product?.title)" :to="`${product?.url}`">
      <img src="/assets/images/nophoto.jpg" alt="product-image">
    </NuxtLink>
    <NuxtLink :title="cleanText(product?.title)" class="products__link" :to="`${product?.url}`" itemprop="url">
      <span itemprop="name">{{ cleanText(product?.title) }}</span>
    </NuxtLink>
<!--    <div v-if="product?.features.length">-->
<!--      <p class="text-sm" v-for="(product, i) in  product?.features" :key="i">{{product?.title}}: <span >{{product?.description}}</span> </p>-->
<!--    </div>-->
<!--    <p v-if="product?.sku.length" class="border-t  mt-auto border-gray-200">-->
<!--      <div class="text-sm flex justify-between mb-2" v-for="sku in  product?.sku" :key="sku.id" itemscope itemprop="offers" itemtype="http://schema.org/Offer">-->
<!--        <p>{{sku?.title}}</p>-->
<!--        <p>-->
<!--          <span itemprop="priceCurrency" content="RUB"></span>-->
<!--          <span itemprop="price">{{sku?.price}}</span> ₽-->
<!--        </p>-->
<!--      </div>-->
<!--    </p>-->
    <div class="mt-auto mb-2 flex gap-2 justify-between">
<!--      <UButton v-if="product?.sku[0]?.price" icon="i-solar-cart-3-outline" class="btn btn-primary mb-2 md:mb-0" @click.prevent="addToCart">Добавить</UButton>-->
<!--      <UButton v-else class="btn btn-primary" @click.prevent="emit('openModal', 'Оставьте заявку')">Оставить заявку</UButton>-->
      <button v-if="product?.sku[0]?.price" class="btn bg-gray-100">от {{product?.sku[0]?.price}} ₽</button>
      <button v-if="product?.sku[0]?.price" class="btn btn-primary">Подробнее</button>
    </div>

  </li>
</template>

<style scoped>

</style>
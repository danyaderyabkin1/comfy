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
    domain: 'b.otellica.ru',
    productId: props.product?.id,
    skuId: props.product?.sku[0]?.id,
    quantity: 1
  }]
})

// Вычисляемое свойство для определения opacity
const productOpacity = computed(() => {
  // Ищем поле с field_title = "notInStock"
  const notInStockField = props.product.fields?.find(
      field => field.field_title === "notInStock"
  );

  // Если поле найдено и оно имеет какое-то значение, возвращаем true
  // Можно настроить логику в зависимости от значения field_value если нужно
  return !!notInStockField;
});

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
<!--  <pre>{{product}}</pre>-->
  <li :class="{'opacity': productOpacity}">
    <NuxtLink v-if="product?.preview_image"  :to="product?.url">
      <img :src="product?.preview_image" alt="product-image">
    </NuxtLink>
    <NuxtLink v-else :to="product?.url">
      <img src="/assets/images/nophoto.jpg" alt="product-image">
    </NuxtLink>
    <NuxtLink class="products__link" :to="product?.url">{{ cleanText(product?.preview_content) }}</NuxtLink>

    <div class="mt-auto">
      <strong v-if="product.sku[0]?.price">{{ product.sku[0]?.price }}
        <span v-if="product.sku[0]?.price">₽</span>
      </strong>
      <button v-if="!product?.sku[0]?.price" class="btn btn-primary w-full" @click="$emit('openModal','Получить каталог', 109)">Получить каталог</button>
      <button v-else-if="product?.sku[0]?.price && !productOpacity" class="btn btn-second w-full" @click="$emit('openModal','Скачать каталог', 109)">Скачать каталог</button>
      <button v-else class="btn btn-second w-full">Нет в наличии</button>
    </div>
    <div class="btn-wrapper flex-col mb-2">
      <button v-if="!productOpacity" class="btn btn-primary text-[12px] w-full" @click="$emit('openModal','Получить образец', 110)">Получить образец</button>
<!--      <button v-if="product?.sku[0]?.price && !productOpacity" class="btn btn-primary flex items-center gap-1 w-full mb-2 md:mb-0" @click.prevent="addToCart"><UIcon name="i-solar-cart-3-outline" size="18"/> Добавить в заказ</button>-->

    </div>
  </li>
</template>

<style scoped>
.opacity {
  opacity: 0.6;
  /* Дополнительные стили для товара, которого нет в наличии */
}
</style>
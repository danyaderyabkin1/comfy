<script setup lang="ts">
const router = useRouter()
const route = useRoute()
const props = defineProps({
  title: {
    type: String,
    required: false
  },
  description: {
    type: String,
    required: false
  },
  gridFour: {
    type: Boolean,
    required: false
  },
  categoryId: {
    type: Number,
    required: true
  },
  containImages: {
    type: Boolean,
    required: false
  },
})
const toast = useToast()

function showToast(title, color) {
  toast.add({title: title, color: color})
}


const {fetchCategories} = useCategories()
const { data: mainCategories } = await useAsyncData('categories', async () => {
  const categories = await fetchCategories();
  const withSubs = await Promise.all(
      categories.map(async cat => ({
        ...cat,
        subCategories: await fetchCategories(cat.id)
      }))
  );
  return { categories: withSubs };
});

const sortDirS = ref(route.query.sortDir || 'desc');
const sortByS = ref(route.query.sortBy || '')
const titleModalForm = ref('Скачать каталог')
const formId = ref(109)
const isOpen = ref(false)
const isHaveFilter = ref(true)
const {fetchProducts} = useProducts();
const {data: products, refresh} = useAsyncData(
    `products-${props.categoryId}`,
    () => fetchProducts(props.categoryId, sortByS.value, sortDirS.value),
    {watch: [() => props.categoryId]}
);
const setModalTitle = (title: string, id: number): void => {
  formId.value = id
  isOpen.value = true;
  titleModalForm.value = title
}

// Добавляем рефы для ценового диапазона
const minPrice = ref<number | null>(null)
const maxPrice = ref<number | null>(null)

// Вычисляем минимальную и максимальную цены из продуктов
const priceRange = computed(() => {
  if (!products.value?.length) return { min: 0, max: 0 }

  // Получаем все цены из sku
  const prices = products.value.flatMap(product =>
      product.sku?.map(sku => sku.price) || []
  ).filter(price => price !== undefined)

  if (prices.length === 0) return { min: 0, max: 0 }

  return {
    min: Math.min(...prices),
    max: Math.max(...prices)
  }
})

const filterFeatures = computed(() => {
  return products?.value?.flatMap(product => product.features || [])
      .reduce((acc, feature) => {
        if (!acc.some(item => item.title === feature.title)) {
          acc.push(feature)
        }
        return acc
      }, [])
})

const groupedFeatures = computed(() => {
  if (!products.value) return {}

  // Создаем объект для группировки
  const groups: Record<string, Set<string>> = {}

  // Проходим по всем продуктам и их характеристикам
  products.value.forEach(product => {
    product.features?.forEach(feature => {
      if (!groups[feature.title]) {
        groups[feature.title] = new Set()
      }
      // Разделяем значения по запятым и добавляем в Set (для уникальности)
      feature.description?.split(',').forEach(value => {
        groups[feature.title].add(value.trim())
      })
    })
  })

  // Преобразуем Set в массив для удобства отображения
  const result: Record<string, string[]> = {}
  Object.keys(groups).forEach(key => {
    result[key] = Array.from(groups[key]).filter(Boolean)
  })

  return result
})

// Функция для обновления URL с выбранными фильтрами
const updateUrlWithFilters = () => {
  const selected = Object.keys(selectedFeatures.value)
      .filter(key => selectedFeatures.value[key])

  if (selected.length > 0) {
    router.push({
      query: {
        ...route.query,
        features: encodeURIComponent(JSON.stringify(selectedFeatures.value))
      }
    })
  } else {
    // Удаляем параметр features если фильтров нет
    const { features, ...query } = route.query
    router.push({ query })
  }
}

const refreshProducts = async (sortBy, sortDir) => {
  console.log('da')
  sortDirS.value = sortDir;
  sortByS.value = sortBy;
  await refresh();
}


// Инициализируем selectedFeatures из query параметров
const selectedFeatures = ref<Record<string, boolean>>(
    route.query.features
        ? JSON.parse(decodeURIComponent(route.query.features as string))
        : {}
)

const handleFeatureToggle = (key: string, isChecked: boolean) => {
  selectedFeatures.value = {
    ...selectedFeatures.value,
    [key]: isChecked
  }
  updateUrlWithFilters()
}

// Обновляем фильтрацию продуктов с учетом цены
const filteredProducts = computed(() => {
  let result = products.value || []

  // Фильтрация по характеристикам
  const selectedFeaturesList = Object.keys(selectedFeatures.value)
      .filter(key => selectedFeatures.value[key])

  if (selectedFeaturesList.length > 0) {
    result = result.filter(product => {
      // Проверяем, что продукт содержит все выбранные характеристики
      return selectedFeaturesList.every(selected => {
        const [title, value] = selected.split(':')
        return product.features?.some(f =>
            f.title === title && f.description?.includes(value)
        )
      })
    })
  }

  // Фильтрация по цене (если есть sku)
  if (minPrice.value !== null || maxPrice.value !== null) {
    result = result.filter(product => {
      // Проверяем все sku товара
      return product.sku?.some(sku => {
        const price = sku.price
        // Проверяем только минимальную цену, если maxPrice не задан
        if (maxPrice.value === null) {
          return minPrice.value === null || price >= minPrice.value
        }
        // Проверяем оба условия, если maxPrice задан
        const minValid = minPrice.value === null || price >= minPrice.value
        const maxValid = price <= maxPrice.value
        return minValid && maxValid
      })
    })
  }

  return result
})

onMounted(() => {
  if (route.query.features) {
    try {
      const features = JSON.parse(decodeURIComponent(route.query.features as string))
      selectedFeatures.value = features
    } catch (e) {
      console.error('Error parsing features from URL', e)
    }
  }
})

// Функция для обновления URL с ценовым фильтром
const updatePriceFilter = () => {
  const query: Record<string, any> = { ...route.query }

  if (minPrice.value !== null) {
    query.minPrice = minPrice.value
  } else {
    delete query.minPrice
  }

  if (maxPrice.value !== null) {
    query.maxPrice = maxPrice.value
  } else {
    delete query.maxPrice
  }

  router.push({ query })
}

// Добавляем computed для проверки наличия sku в продуктах
const hasProductsWithSku = computed(() => {
  return products.value?.some(product => product.sku?.length) || false
})

// Обработчик изменения цены
const handlePriceChange = () => {
  // Если поле пустое, устанавливаем null
  if (minPrice.value === '') minPrice.value = null
  if (maxPrice.value === '') maxPrice.value = null

  updatePriceFilter()
  refreshProducts(sortByS.value, sortDirS.value)
}


// Инициализация при монтировании
onMounted(() => {
  isHaveFilter.value = window.innerWidth >= 992
})


onMounted(() => {
  if (route.query.minPrice) {
    minPrice.value = Number(route.query.minPrice)
  }
  if (route.query.maxPrice) {
    maxPrice.value = Number(route.query.maxPrice)
  }
})


// При изменении route.query обновляем фильтры
watch(() => route.query.features, (newVal) => {
  if (newVal) {
    try {
      const features = JSON.parse(decodeURIComponent(newVal as string))
      selectedFeatures.value = features
    } catch (e) {
      console.error('Error parsing features from URL', e)
    }
  } else {
    selectedFeatures.value = {}
  }
})

watch(isHaveFilter, (val) => {
  console.log('isHaveFilter changed to:', val)
})
</script>

<template>
  <section class="products">
    <div class="container products__container">

      <h1 class="text-center">{{title}}</h1>
      <!--      <pre>{{products}}</pre>-->
<!--      <Sort v-if="products?.length" @refresh="refreshProducts" @open-filter="isHaveFilter = !isHaveFilter"/>-->
      <div class="products__wrapper">
<!--        <aside v-if="isHaveFilter" class="aside">-->
<!--          <h4 class="text-2xl border-b border-b-gray-200 pb-3 ">Фильтр</h4>-->

<!--          <div v-if="Object.keys(groupedFeatures).length" class="py-3">-->
<!--            <h5 class="font-semibold mb-2">Характеристики</h5>-->
<!--            <div v-for="(values, title) in groupedFeatures" :key="title" class="mb-4">-->
<!--              <h6 class="font-medium mb-2">{{ title }}</h6>-->
<!--              <div class="flex flex-wrap gap-2">-->
<!--                <label-->
<!--                    v-for="(value, i) in values"-->
<!--                    :key="i"-->
<!--                    class="flex items-center gap-2 cursor-pointer px-3 py-1 bg-gray-100 rounded-full"-->
<!--                >-->
<!--                  <UCheckbox-->
<!--                      color="neutral"-->
<!--                      :model-value="!!selectedFeatures[`${title}:${value}`]"-->
<!--                      @update:model-value="(val) => handleFeatureToggle(`${title}:${value}`, val)"-->
<!--                  />-->
<!--                  <span>{{ value }}</span>-->
<!--                </label>-->
<!--              </div>-->
<!--            </div>-->
<!--          </div>-->

<!--          <div v-if="hasProductsWithSku" class="price-filter py-3 mb-6">-->
<!--            <h5 class="font-semibold mb-2">Цена</h5>-->
<!--            <div class="flex items-center gap-2">-->
<!--              <UInput-->
<!--                  color="yellow"-->
<!--                  type="text"-->
<!--                  placeholder="От"-->
<!--                  v-model="minPrice"-->
<!--                  @update:model-value="handlePriceChange"-->
<!--                  :min="0"-->
<!--                  :max="maxPrice || priceRange.max"-->
<!--              />-->
<!--              <span>-</span>-->
<!--              <UInput-->
<!--                  color="yellow"-->
<!--                  type="text"-->
<!--                  placeholder="До"-->
<!--                  v-model="maxPrice"-->
<!--                  @update:model-value="handlePriceChange"-->
<!--                  :min="minPrice || 0"-->
<!--                  :max="priceRange.max"-->
<!--              />-->
<!--            </div>-->
<!--            <div class="text-xs text-gray-500 mt-1">-->
<!--              Диапазон: {{ priceRange.min }} ₽ - {{ priceRange.max }} ₽-->
<!--            </div>-->
<!--          </div>-->

<!--          <ul class="flex flex-col gap-2">-->
<!--            <li class="" v-for="category in mainCategories?.categories" :key="category.id">-->
<!--              <NuxtLink class="btn btn-white flex justify-between items-center" :to="category.url">-->
<!--                {{category.title}}-->
<!--              </NuxtLink>-->
<!--              <SubMenu :subCategory="category?.subCategories"/>-->
<!--            </li>-->
<!--          </ul>-->
<!--        </aside>-->

        <ul :class="{'four-columns': gridFour, 'image-contain': containImages}" class="products__list four-columns">
          <ProductsListItem
              v-for="product in filteredProducts"
              :key="product?.id"
              :product="product"
              @open-modal="setModalTitle"
              @add-to-cart="showToast"
          />
        </ul>
      </div>
      <UModal v-model="isOpen"
              :ui="{ container: 'items-start pt-14 bg-white sm:bg-gray-50/50', shadow: 'shadow-none sm:shadow-lg', padding: 'p-0 sm:p-0', rounded: 'rounded-none sm:rounded-lg' }"
              class="modal">
        <div class="px-6 py-10">
          <UButton
              color="gray" variant="ghost" icon="i-heroicons-x-mark-20-solid" class="-my-1 modal__close" @click.prevent="isOpen = false"/>
          <TheModalForm :form-id="formId" :title="titleModalForm"/>
        </div>
      </UModal>
    </div>
  </section>
</template>
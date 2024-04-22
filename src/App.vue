<script setup lang="ts">
import { onMounted, ref, computed } from 'vue'
import ProductItem from './components/ProductItem.vue'
import ItemCartPreview from './components/ItemCartPreview.vue'

const product = ref()
const cart: any = ref([])

const showCart = ref(false)

/*
 * Retrieve product information
 */
onMounted(async () => {
  await fetch(import.meta.env.VITE_PRODUCT)
    .then((response) => response.json())
    .then((data): any => {
      product.value = data
    })
})

const cartSize = computed(() => {
  return cart.value.length
})

const addProductToCart = (item: any) => {
  cart.value.push(item)
  console.log(cart.value)
}

const openCart = () => {
  showCart.value = true
}
</script>

<template>
  <header>
    <span @click="openCart">My Cart ({{ cartSize }})</span>
  </header>

  <main>
    <ProductItem :product="product" @add-product-to-cart="(item) => addProductToCart(item)" />
    <div v-if="showCart">
      <ItemCartPreview v-for="item in cart.value" :key="item" :item="item" />
    </div>
  </main>
</template>

<style scoped>
header {
  background-color: var(--color-header-background);
  padding: 0.2rem var(--padding-sides);
  font-size: 0.7rem;
  text-align: right;
}
header > span:hover {
  cursor: pointer;
}
main {
  padding: 2rem var(--padding-sides);
}
@media screen and (max-width: 800px) {
  header {
    padding: 0.2rem var(--padding-sides-small);
  }
  main {
    padding: 2rem var(--padding-sides-small);
  }
}
/*
@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
} */
</style>

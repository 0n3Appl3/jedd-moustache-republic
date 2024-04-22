<script setup lang="ts">
import { onMounted, ref, computed } from 'vue'
import ProductItem from './components/ProductItem.vue'

const product = ref()
const cart: any = ref([])

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
</script>

<template>
  <header>
    <span>My Cart ({{ cartSize }})</span>
  </header>

  <main>
    <ProductItem :product="product" @add-product-to-cart="(item) => addProductToCart(item)"/>
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

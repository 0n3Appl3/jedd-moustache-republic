<script setup lang="ts">
import { onMounted, ref } from 'vue'
import ProductItem from './components/ProductItem.vue'

const product = ref()

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
</script>

<template>
  <header>
    <span>My Cart (0)</span>
  </header>

  <main>
    <ProductItem :product="product" />
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

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
  let size = 0
  if (getCartItems.value.length === 0) {
    return 0
  }
  for (let i = 0; i < getCartItems.value.length; i++) {
    size += getCartItems.value[i].quantity
  }
  return size
})

const addProductToCart = (item: any) => {
  if (getCartItems.value.length === 0) {
    cart.value.push(item)
    return
  }
  for (let i = 0; i < getCartItems.value.length; i++) {
    if (getCartItems.value[i].title === item.title && getCartItems.value[i].size === item.size) {
      getCartItems.value[i].quantity++
      return
    }
  }
  cart.value.push(item)
}

const toggleCart = () => {
  showCart.value = !showCart.value
}

const getCartItems = computed(() => {
  return cart.value
})
</script>

<template>
  <header>
    <div @click="toggleCart">My Cart ({{ cartSize }})</div>
    <div v-if="showCart" class="cart__container">
      <ItemCartPreview v-for="item in getCartItems" :key="item" :item="item" />
    </div>
  </header>

  <main>
    <ProductItem :product="product" @add-product-to-cart="(item) => addProductToCart(item)" />
  </main>
</template>

<style scoped>
header {
  background-color: var(--color-header-background);
  padding: 0.2rem var(--padding-sides);
  font-size: 0.7rem;
  text-align: right;
}
header > div:hover {
  cursor: pointer;
}
main {
  position: relative;
  padding: 2rem var(--padding-sides);
}
.cart__container {
  position: absolute;
  right: var(--padding-sides);
  min-width: 300px;
  padding: 1rem;
  float: right;
  text-align: left;
  border: 1px solid var(--color-border-light);
  background-color: var(--color-background);
  z-index: 99;
}
@media screen and (max-width: 800px) {
  header {
    padding: 0.2rem var(--padding-sides-small);
  }
  main {
    padding: 2rem var(--padding-sides-small);
  }
  .cart__container {
    right: var(--padding-sides-small);
  }
}
</style>

<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps({
  title: {
    type: String
  },
  description: {
    type: String
  },
  price: {
    type: Number
  },
  image: {
    type: String
  }
})

const formattedPrice = computed(() => {
  return props.price?.toLocaleString('en-NZ', {
    style: 'currency',
    currency: 'NZD',
  })
})
</script>

<template>
  <div class="product__container">
    <div class="product__image">
      <img :src="props.image" alt="Product Image" />
    </div>
    <div class="product__content">
      <p class="product__content-title">{{ title }}</p>
      <hr />
      <p class="product__content-price">{{ formattedPrice }}</p>
      <hr />
      <p class="product__content-description">{{ description }}</p>
    </div>
  </div>
</template>

<style scoped>
.product__container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  justify-self: center;
  padding: 2rem var(--padding-sides);
}
.product__image > img {
  height: 500px;
}
.product__content > hr {
  border: 1px solid var(--color-header-background);
}
.product__content-title {
  font-size: 1.3rem;
  color: var(--color-text-dark);
  margin-bottom: 1rem;
}
.product__content-price {
  font-weight: bold;
  color: var(--color-text-dark);
  margin: 0.3rem 0;
}
.product__content-description {
  font-size: 0.8rem;
  margin-top: 1rem;
}
</style>

<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps({
  product: {
    type: Object
  },
})

const formattedPrice = computed(() => {
  return props.product?.price.toLocaleString('en-NZ', {
    style: 'currency',
    currency: 'NZD',
  })
})
</script>

<template>
  <div class="product__container">
    <div class="product__image">
      <img :src="props.product?.imageURL" alt="Product Image" />
    </div>
    <div class="product__content">
      <p class="product__content-title">{{ product?.title }}</p>
      <hr />
      <p class="product__content-price">{{ formattedPrice }}</p>
      <hr />
      <p class="product__content-description">{{ product?.description }}</p>

      <p class="product__content-size">Size
        <span class="product__content-required">*</span>
      </p>
      <div class="product__content-size-button" v-for="size in product?.sizeOptions" :key="size.id">
        {{ size.label }}
      </div>
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
.product__content-required {
  color: var(--color-required-star);
}
.product__content-size {
  font-size: 0.7rem;
  font-weight: bold;
  letter-spacing: 0.1rem;
  text-transform: uppercase;
  margin-top: 2rem;
  margin-bottom: 0.5rem;
}
.product__content-size-button {
  display: inline-block;
  font-size: 0.7rem;
  border: 1px solid var(--color-size-buttons);
  padding: 0.8rem 1.2rem;
  margin-right: 0.5rem;
}
.product__content-size-button:hover {
  cursor: pointer;
}
</style>

<script setup lang="ts">
import { computed, ref } from 'vue'

const props = defineProps({
  product: {
    type: Object
  }
})
const emit = defineEmits(['addProductToCart'])

const sizeButtonClass = ref('product__size-button')
const sizeButtonSelectedClass = ref('product__size-button--selected')

const selectedSize = ref(null)
const showError = ref(false)

const formattedPrice = computed(() => {
  return props.product?.price.toLocaleString('en-NZ', {
    style: 'currency',
    currency: 'NZD'
  })
})

const selectSize = (event: any) => {
  const clickedSize = event.target
  if (clickedSize.classList.contains(sizeButtonSelectedClass.value)) {
    clickedSize.classList.remove(sizeButtonSelectedClass.value)
    clickedSize.classList.add(sizeButtonClass.value)
    selectedSize.value = null
    return
  }
  try {
    // Remove previously-selected size
    let button = document.getElementsByClassName(sizeButtonSelectedClass.value)[0]
    button.classList.remove(sizeButtonSelectedClass.value)
    button.classList.add(sizeButtonClass.value)
  } catch (error) {
    /* empty */
  }
  clickedSize.classList.remove(sizeButtonClass.value)
  clickedSize.classList.add(sizeButtonSelectedClass.value)
  selectedSize.value = clickedSize.textContent
  showError.value = false
}

const addToCart = () => {
  if (!selectedSize.value) {
    showError.value = true
    return
  }
  emit('addProductToCart', {
    title: props.product?.title,
    price: formattedPrice.value,
    size: selectedSize.value,
    quantity: 1,
    image: props.product?.imageURL
  })
}
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

      <p class="product__content-size">
        Size
        <span class="product__content-required">*</span>
      </p>
      <p v-if="showError" class="product__content-required">
        You must selected a size to add this item to cart.
      </p>
      <div
        :class="sizeButtonClass"
        v-for="size in product?.sizeOptions"
        :key="size.id"
        @click="selectSize"
      >
        {{ size.label }}
      </div>

      <button class="product__add-to-cart-button" @click="addToCart">Add to Cart</button>
    </div>
  </div>
</template>

<style scoped>
.product__container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  justify-self: center;
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
.product__size-button,
.product__size-button--selected {
  display: inline-block;
  font-size: 0.7rem;
  border: 1px solid var(--color-border-light);
  padding: 0.8rem 1.2rem;
  margin-right: 0.5rem;
}
.product__size-button--selected {
  color: var(--color-border-dark);
  border-color: var(--color-border-dark);
}
.product__size-button:hover,
.product__size-button--selected:hover,
.product__add-to-cart-button:hover {
  cursor: pointer;
}
.product__add-to-cart-button {
  display: block;
  font-size: 0.8rem;
  font-weight: bold;
  text-transform: uppercase;
  color: var(--color-border-dark);
  background-color: var(--color-background);
  border: 2px solid var(--color-border-dark);
  padding: 0.8rem 1.4rem;
  margin-top: 1.5rem;
  transition: all 0.2s ease-in-out;
}
.product__add-to-cart-button:hover {
  background-color: var(--color-border-dark);
  color: var(--color-background);
}
@media screen and (max-width: 800px) {
  .product__container {
    display: block;
  }
  .product__image > img {
    width: 100%;
    height: auto;
  }
}
</style>

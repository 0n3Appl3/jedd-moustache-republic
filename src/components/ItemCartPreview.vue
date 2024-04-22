<script setup lang="ts">
const props = defineProps({
  item: {
    type: Object
  }
})
</script>

<template>
  <div class="item__container">
    <div class="item__image">
      <img :src="props.item?.image" alt="Item Image" />
    </div>
    <div class="item__content">
      <p class="item__title">{{ props.item?.title }}</p>
      <p class="item__price">
        {{ props.item?.quantity }}x <span>{{ props.item?.price }}</span>
      </p>
      <p class="item__size">Size: {{ props.item?.size }}</p>
    </div>
  </div>
</template>

<style scoped>
p {
  color: var(--color-text-dark);
}
p > span {
  font-weight: bold;
}
.item__container {
  display: grid;
  grid-template-columns: 1fr 2fr;
  justify-self: center;
}
.item__image > img {
  height: 100px;
}
</style>

<script setup lang="ts">
import { computed, ref } from 'vue'

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
        {{ props.item?.quantity }}x <strong>{{ props.item?.price }}</strong>
      </p>
      <p class="item__size">Size: {{ props.item?.size }}</p>
    </div>
  </div>
</template>

<style scoped>
.item__container {
  display: block;
}
</style>

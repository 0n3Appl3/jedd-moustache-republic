<script setup lang="ts">
import { ref } from 'vue'

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
</script>

<template>
  <p>{{ title }}</p>
  <p>{{ description }}</p>
  <p>{{ price }}</p>
  <img :src="props.image" alt="Product Image" />
</template>

<style scoped></style>

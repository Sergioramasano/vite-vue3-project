<template>
<div class="item">
  <p>{{name}}</p>
  <p>
    <yummy-meal-price :price="price" />
  </p>
  <button @click="addToCart" class="btn btn-secondary">Add to cart</button>
</div>
</template>

<script setup>
import YummyMealPrice from './YummyMealPrice.vue'
const props = defineProps({
  name: {
      type: String,
      required: true,
  },
  price: {
    type: Number,
    required: true,
  }
})
  const emit = defineEmits(["addToCart"])
 const addToCart = () => emit("addToCart", props.name)
</script>

<style scoped>
  .item {
    background: rgba(235, 214, 95, 0.479);
    border-radius: 3px;
    padding: 2rem;
  }
</style>

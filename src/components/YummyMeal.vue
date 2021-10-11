<template>
<div class="item">
  <span v-if="meal.quantity" class="badge badge-danger">
    {{meal.quantity}}
  </span>
  <p>{{meal.name}}</p>
  <p>
    <yummy-meal-price :price="meal.price" />
  </p>
  <button @click="addToCart" class="btn btn-secondary">Add to cart</button>
</div>
</template>

<script setup lang="ts">
import YummyMealPrice from './YummyMealPrice.vue'
const props = defineProps({
  meal:{
    type: Object,
    required: true
  }
})
 const emit = defineEmits(["addToCart"])
 const addToCart = () => {
   emit("addToCart", props.meal.id)
  }
</script>

<style scoped>
  .item {
    background: rgba(235, 214, 95, 0.479);
    border-radius: 3px;
    padding: 2rem;
    position: relative;
  }
  .badge {
    position: absolute;
    right: .5rem;
    top: .5rem;
  }
</style>

<template>
   <nav class="navbar navbar-dark">
      <button @click="toggleCartModal" class="btn btn-outline-danger navbar-brand">
       cart 
       <span class="badge badge-danger">
         {{counter}}
        </span>
      </button>
    </nav>
</template>
<script setup>
  import { computed } from 'vue'
  const props = defineProps({
      meals: {
        type: Array,
        required: true
      }
  })
  let counter = computed(() => props.meals.reduce((acc, item)=>acc + item.quantity, 0))
  const emit = defineEmits(["toggleCartModal"])
  const toggleCartModal = () => emit("toggleCartModal")
</script>


<style scoped>
  .navbar {
    position: relative;
    top: 0;
    justify-content: flex-end;
  }
</style>
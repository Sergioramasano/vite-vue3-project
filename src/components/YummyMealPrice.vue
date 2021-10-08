<template>
  <strong>{{pricePretty}}</strong>
</template>

<script setup lang="ts">
  import {computed, ComputedRef, inject} from "vue"
  const props = defineProps({
    price: {
        type: Number,
        required: true,
      }
  })
  const currencySymbol = inject("currencySymbol")
  const pricePretty : ComputedRef<string> = computed(()=>`${currencySymbol.value}${props.price.toFixed(2)}`)
</script>

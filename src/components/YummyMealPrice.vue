<template>
  <strong>{{pricePretty}}</strong>
</template>

<script setup>
  import {computed, inject} from "vue"
  const props = defineProps({
    price: {
        type: Number,
        required: true,
      }
  })
  const currencySymbol = inject("currencySymbol")
  const pricePretty = computed(()=>`${currencySymbol.value}${props.price.toFixed(2)}`)
</script>

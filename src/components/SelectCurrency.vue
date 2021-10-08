<template>
  <label class="label" for="currencySymbol">Choose currency:</label>
  <select 
    :value="currencySymbol" 
    id="currencySymbol" 
    class="d-block m-auto p-2 pr-5" 
    :placeholder="currencySymbol"
    @input="$emit('update:currencySymbol', $event.target.value)"
  >
    <option 
      v-for="currency of currencyArray" 
      :key="currency.value" 
      :value="currency.value"
    >
      {{currency.title}}
    </option>
  </select>
</template>
<script setup lang="ts">
  const props = defineProps({
      currencySymbol: {
        type: String,
        required: true
      }
  })
  const currencyArray : { title: string; value: string }[] = [
      {title: 'Dollar $', value: '$'},
      {title: 'Sobaka @', value: '@'},
      {title: 'Star *', value: '*'},
  ]
</script>

<style scoped>
  #currencySymbol, .label {
    color:tomato;
    font-weight: 900;
  }
  #currencySymbol {
    background: grey;
  }
</style>

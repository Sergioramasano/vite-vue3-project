

<template>
  <main class="app">
    <h1 class="title"> hello {{name}}</h1>
    <select-currency v-model:currencySymbol="currencySymbol" />
    <section class="d-flex justify-content-around flex-wrap wrapper mt-4">
      <yummy-meal 
        v-for="food of meals" 
        :key="food.name" 
        :name="food.name" 
        :price="food.price" 
        @addToCart="addItemToCart" 
      />
    </section>
  </main>
</template>

<script setup>
  import YummyMeal from './components/YummyMeal.vue'
  import {ref, reactive, watch, provide} from "vue"
  import SelectCurrency from './components/SelectCurrency.vue'
    const currencySymbol = ref("$")
      provide("currencySymbol", currencySymbol)
    
    const name = ref("The army burger")
    const meal = reactive({name: "Burger", price: 120})
    const meals = reactive([
      {name: "Burger", price: 120},
      {name: "Cheese", price: 140},
      {name: "Lodash", price: 0},
      {name: "Fries", price: 40},
    ])
    const cart = reactive([])
    const addItemToCart = (item) => cart.push(item)
    watch(
      [()=>[...cart]], 
      (newValue, oldValue)=>console.log(newValue, oldValue)
      )
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  
  background: #2c3e5038;
  height: 100vh;
}

.app {
  background-image: url('./src/assets/vector.jpeg');
  height: 100vh;
  padding-top: 60px;
}

.app .title {
  color: whitesmoke;
  font-weight: 900;
  text-transform: uppercase;
}

.wrapper {
  padding: 2rem;
  background: #2c3e50;
}
</style>

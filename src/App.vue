<template>
  <main class="app">
   <navbar 
      @toggleCartModal="toggleCartModal"
      :meals="meals"
    />
    <h1 class="title"> hello {{name}}</h1>
    <transition name="fade">
      <shopping-cart 
        v-if="isCartModalVisible" 
        @toggleCartModal="toggleCartModal" 
        @removeItemFromCart="removeItemFromCart"
        :cart="meals" 
      />
    </transition>
    
    <select-currency 
      v-model:currencySymbol="currencySymbol" 
    />
    <section class="d-flex justify-content-around flex-wrap wrapper mt-4">
      <yummy-meal 
        v-for="food of meals" 
        :key="food.id" 
        :meal="food" 
        @addToCart="addItemToCart" 
      />
    </section>
  </main>
</template>

<script setup lang="ts">
  import YummyMeal from './components/YummyMeal.vue'
  import {ref, reactive, watch, provide} from "vue"
  import SelectCurrency from './components/SelectCurrency.vue'
  import ShoppingCart from './components/ShoppingCart.vue'
  import Navbar from './components/Navbar.vue'
  import {Imeal} from './interfaces/interfaces'
    const currencySymbol = ref<string>("$")
      provide("currencySymbol", currencySymbol)
    
    const name = ref<string>("The army burger")
    const isCartModalVisible = ref(false)
    const meals = ref< Imeal[] >([
      {name: "Burger", price: 120, id: 11, quantity: 0},
      {name: "Cheese", price: 140, id: 12, quantity: 0},
      {name: "Lodash", price: 0, id: 13, quantity: 0},
      {name: "Fries", price: 40, id: 14, quantity: 0},
    ])
    const addItemToCart = (id : number) => {
      let currentItem = meals.value.find(item=>item.id===id)
      currentItem.quantity+=1
    }
    const removeItemFromCart = (id : number) =>{
    let currentItem = meals.value.find(item=>item.id===id)
     if(currentItem.quantity>0) {
       currentItem.quantity-=1
     }
    } 
    const toggleCartModal =()=>isCartModalVisible.value = !isCartModalVisible.value
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

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
  opacity: 0;
}
</style>

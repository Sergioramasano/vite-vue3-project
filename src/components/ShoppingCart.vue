<template>
<div class="modal bg-dark" role="dialog">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Your shopping cart</h5>
        <button 
          @click="toggleCartModal" 
          type="button" 
          class="close" 
          aria-label="Close"
        >
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        <table v-if="cart.length"  class="table">
          <thead>
            <tr>
              <th >Name</th>
              <th >Price</th>
              <th >Count</th>
              <th></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item of cart" :key="item.id">
              <th >{{item.name}}</th>
              <td>{{item.price}}</td>
              <th>{{item.quantity}}</th>
              <td>
                <button 
                  v-if="item.quantity>0" 
                  @click="removeItemFromCart(item.id)" 
                  class="btn btn-danger remover">
                    x
                </button>
                <span v-else>-</span>
              </td>
            </tr>
          </tbody>
        </table>
        <h3 v-else>No data!</h3>
      </div>
      <div class="modal-footer">
        <button @click="toggleCartModal" type="button" class="btn btn-secondary">Close</button>
      </div>
    </div>
  </div>
</div>
</template>
<script setup lang="ts">
  const props = defineProps({
      cart: {
        type: Array,
        required: true
      }
  })
  const emit = defineEmits(["toggleCartModal", "removeItemFromCart"])
  const toggleCartModal = () => emit("toggleCartModal")
  const removeItemFromCart = (id:number) => emit("removeItemFromCart", id)
</script>

<style scoped>
 .modal {
   display: block;
 }
 .modal .table td, .modal .table th {
   vertical-align: middle;
 }
 .modal .remover {
   padding: 0 1rem;
 }
</style>

<template>
  <div class="main-content">
    <div class="desserts">
      <p style="font-size: 2em; font-weight: 600; color: #25231b;">Desserts</p>

      <div class="products-main-container">
        <ProductCart v-for="produto in 10" :key="produto" />
      </div>

    </div>

    <div class="cart">
      <p>Your Cart (0)</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import ProductCart from "./components/ProductCart.vue";
</script>

<style scoped>
/* PRATOS */
.main-content {
  height: 100%;
  width: 100%;

  display: flex;
  justify-content: space-between;
  padding: 1rem;
  gap: 2rem;
}

.desserts {
  flex: 1;
  display: flex;
  flex-wrap: wrap;
  justify-content: start;
  align-content: flex-start;

  overflow-y: auto;
  gap: 1rem;
  padding: 1rem;
}


.products-main-container {
  height: 100%;
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  justify-content: center;
}

/* PRATOS - FIM */
.cart {
  width: 30%;
  background-color: orange;
}
</style>
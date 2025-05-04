<template>
  <div class="main-content">
    <div class="desserts">
      <p style="font-size: 2em; font-weight: 600; color: #25231b;">Desserts</p>

      <div class="products-main-container">
        <ProductCart v-for="item in listProducts" :key="item.id" :product="item" @addToCart="handleCardList" />
      </div>
    </div>

    <div class="cart">
      <p style="font-size: 2em; font-weight: 600; color: #F25C05;">Your Cart ({{ listCart.length }})</p>
      <!-- <span class="material-symbols-outlined">shopping_cart_off</span> -->
      <div>
        <div v-for="(item, index) in listCart" :key="item.product.id"
          style="display: flex; justify-content: space-between; border-bottom: solid 0.25px #25231b; padding: 1rem">
          <div>
            <p style="font-weight: 500; color: #25231b;">{{ item.product.title }}</p>
            <section style="display: flex; gap: 1rem; margin-top: 0.5rem;">
              <p style="color: #F25C05; font-weight: 600;">{{ item.quantity }}x</p>
              <p style="font-weight: 300; color: #25231b;">${{ item.product.price.toFixed(2) }}</p>
              <p style="font-weight: 600; color: #25231b;">${{ item.total.toFixed(2) }}</p>
            </section>
          </div>
          <span class="material-symbols-outlined" style="cursor: pointer; align-self: center;"
            @click="remove(index)">cancel</span>
        </div>
      </div>
      <div style="display: flex; justify-content: space-between; margin-top: 1rem; align-items: center;">
        <p style="color: #25231b; font-size: 22px;">Total</p>
        <p style="font-weight: 800; font-size: 32px; color: #25231b;">${{ sumTotal().toFixed(2) }} </p>
      </div>
      <button
        style="background-color: #F25C05;color: white;border: none; padding: 1rem 1rem; border-radius: 32px; margin-top: 1rem; font-weight: 600; cursor: pointer; font-size: 18px;">Confirm Order</button>
    </div>
  </div>
</template>





<script setup lang="ts">
import { ref } from "vue";
import ProductCart from "./components/ProductCart.vue";
import type { IProduct } from "./interface/IProduct";

interface IProductCart {
  product: IProduct;
  quantity: number,
  total: number
}

const listCart = ref<IProductCart[]>([]);

const listProducts: Array<IProduct> = [
  {
    id: 1,
    type: "Pie",
    title: "Lemon Menrigue Pie",
    price: 4.00,
    url_image: "https://www.shutterstock.com/image-photo/fried-salmon-steak-cooked-green-600nw-2489026949.jpg"
  },
  {
    id: 2,
    type: "Dessert",
    title: "Vanilla Bean",
    price: 6.00,
    url_image: "https://thumbs.dreamstime.com/b/omega-food-sources-concrete-background-top-view-copy-space-foods-high-fatty-acids-including-vegetables-seafood-nut-seeds-203687798.jpg"
  }
]

const handleCardList = (newItem: IProduct) => {

  // Verificar se o newItem Já existe no listCart

  const existingItem = listCart.value.find(item => item.product.id === newItem.id);

  // Caso ele não exista
  if (existingItem === undefined) {
    //adicionamos
    listCart.value.push({
      product: newItem,
      quantity: 1,
      total: newItem.price,
    })
  } else {
    existingItem.quantity++;
    existingItem.total += newItem.price;
  }
}

const sumTotal = () => {
  let total = 0;
  listCart.value.forEach(item => {
    total += item.total;
  })
  return total;
}

const remove = (index: number) => {
  listCart.value.splice(index, 1);
}


</script>

<style scoped>
/* PRATOS */
.main-content {
  background-color: #FAF0E6;
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
  display: flex;
  flex-direction: column;
  padding: 1rem;
  width: 25%;
  background-color: white;
  border-radius: 1rem;
  height: min-content;
}
</style>
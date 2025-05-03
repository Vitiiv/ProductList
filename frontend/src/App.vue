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
          style="display: flex; justify-content: space-between; border-bottom: solid 1px black; padding: 1rem">
          <div>
            <p>{{ item.product.title }}</p>
            <section style="display: flex; gap: 1rem; margin-top: 0.5rem;">
              <p>{{ item.quantity }}x</p>
              <p>${{ item.product.price.toFixed(2) }}</p>
              <p>${{ item.total.toFixed(2) }}</p>
            </section>
          </div>
          <span class="material-symbols-outlined" style="cursor: pointer; align-self: center;" @click="remove(index)" >cancel</span>
        </div>
      </div>
      <div style="display: flex; justify-content: space-between; margin-top: 1rem;">
        <p>Total</p>
         <p> {{ sumTotal().toFixed(2) }} </p>
      </div>
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
  width: 30%;
  box-shadow: rgba(0, 0, 0, 0.16) 0px 1px 4px, rgb(51, 51, 51) 0px 0px 0px 3px;
}
</style>
<script setup>
import { computed, ref } from 'vue';
import Button from './components/Button.vue';
import CartsContainer from './components/CartsContainer.vue';
import Header from './components/Header.vue';
import ProductCard from './components/ProductCard.vue';
import ProductCart from './components/ProductCart.vue';

const products = ref([])
const carts = ref([])


// CODE UNTUK FETCH DATA PRODUCT
const fetchProducts = async () => {
  const res = await fetch('https://fakestoreapi.com/products')
  const data = await res.json()
  products.value = data
}

fetchProducts()


// CODE UNTUK MENAMBAHKAN PRODUCT KE CART
const addToCart = (product) => {
  const addedItem = carts.value.find((item) => item.id === product.id)

  if(addedItem) {
    addedItem.quantity++
  } else {
    carts.value.push({
      ...product,
      quantity: 1
    })
  }
}

// CODE UNTUK MENGHAPUS PRODUCT DI CART
const deleteCart = (id) => {
  carts.value = carts.value.filter((cart) => cart.id !== id)
}

//CODE UNTUK MENGHITUNG TOTAL HARGA DI DALAM CART
const totalPrice = computed(() => {
  const total = carts.value.reduce((acc, cart) => {
    return acc + cart.price * cart.quantity;
  }, 0);

  return total.toFixed(2);
})

const navStatus = ref(false)
</script>

<template>
  <div class="p-5 w-full">
    <Header @click="navStatus = true" :totalProduct="carts.length"/>

    <div class="w-full flex justify-between items-start relative">
      <div class="flex flex-wrap gap-5 max-md:w-full max-md:justify-center max-md:mt-5"
       :class="[navStatus ? 'w-8/12' : 'w-full']"
      >
        <ProductCard v-for="product in products" :key="product.id" class="max-md:w-full"
          :title="product.title"
          :price="product.price"
          :img="product.image"
          :alt="product.title"
          @cart="addToCart(product)"
        />
      </div>

      <CartsContainer :open="navStatus" @close="navStatus = false">
        <div class="carts text-gray-600 pt-24 w-full">
          <div class="carts-info fixed flex items-center flex-col top-1 pt-4 w-full">
            <p class="mb-3 text-lg font-semibold">Total Product : {{ carts.length }}</p>
            <Button :text="`Checkout Products : $${totalPrice}`" class="w-10/12"/>
          </div>

          <ProductCart 
            v-for="cart in carts" :key="cart.id"
            :title="cart.title"
            :price="cart.price"
            :img="cart.image"
            :alt="cart.title"
            :quantity="cart.quantity"
            @delete="deleteCart(cart.id)"
            @addQty="cart.quantity++"
            @subQty="() => {
              cart.quantity > 1 ? cart.quantity-- : deleteCart(cart.id)
            }"
          />
        </div>
      </CartsContainer>
    </div>
  </div>
</template>

<style scoped>
</style>

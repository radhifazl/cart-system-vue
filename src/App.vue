<script setup>
import { computed, ref } from 'vue';
import Button from './components/Button.vue';
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
</script>

<template>
  <div class="p-5 w-full">
    <h1 class="text-center text-gray-600 font-bold text-2xl mb-5">Cart System</h1>

    <div class="w-full flex justify-between items-start">
      <div class="flex flex-wrap gap-5 w-5/12 max-md:w-full">
        <ProductCard v-for="product in products" :key="product.id"
          :title="product.title"
          :price="product.price"
          :img="product.image"
          :alt="product.title"
          @cart="addToCart(product)"
        />
      </div>

      <div class="carts text-gray-600">
        <div class="carts-info mb-5">
          <h1 class="text-center font-bold text-2xl mb-5">Cart</h1>
          <p>Total Product : {{ carts.length }}</p>
          <Button :text="`Checkout Products : ${totalPrice}`"/>
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
    </div>
  </div>
</template>

<style scoped>
</style>

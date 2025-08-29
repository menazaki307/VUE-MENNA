<script setup>
import { ref, computed } from 'vue';

import Navbar from './components/Navbar.vue';
import ProductCard from './components/ProductCard.vue';

const products = ref([
  {
    id: 1,
    name: 'T-shirt',
    price: 500,
    inStock: 5, 
    description: 'A collection of T-shirts for all ages .',
    image: 'https://babamisr.com/public/uploads/all/vlM4sHdYMZoChK0sdmGGCI4O8AjVHQdgk4VkLTXM.jpg'
  },
  {
    id: 2,
    name: 'Dresses',
    price: 2000,
    inStock: 3, 
    description: 'Every girl\'s dream evening dress .',
    image: 'https://upload.3dlat.com/uploads/3dlat.net_27_16_a9c4_76cbc214f0933.jpg'
  },
  {
    id: 3,
    name: 'Pants',
    price: 800,
    inStock: 7, 
    description: 'Indescribable beauty .',
    image: 'https://cdn.salla.sa/wWwyOy/2b6842c3-5f33-471f-b448-2996435ad40f-1000x988.88888888889-a2B0MwTq3Q7pKBE8EqCMgyk6iLGCMdppKEgZgpFz.jpg'
  },
  {
    id: 4,
    name: 'Accessories',
    price: 300,
    inStock: 10, 
    description: 'Very beautiful .',
    image: 'https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj6nG79reJlon1qRpruyVlowZh_MsBie58hTMDbVC5xWDbDimwGL215wvLITZaoype58eWKuPLIVTxJphv5e5vUohPRI487FjdkkDwd2XIIKNaMrtDVxwZ8mVBzSAAP0a9BLhdAwqZeCgl1/s16000-rw/c96ea6a839.jpg'
  },
  {
    id: 5,
    name: 'Makeup',
    price: 4000,
    inStock: 2, 
    description: 'Very beautiful .',
    image: 'https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjEgV2WHcusK_6br752PUPNW1DRio6eHdWGdvgZeQsc8So6IaMtlcuMoTg8BkaXwBb66s-2i_hX0FmROxRQiW20ZBZh9Q_TDtEnuqXRN0Xl5WOY8GkWHhxKRDzvaCkBg0Umg90LDK0V9ije/s640/%25D9%2585%25D9%2583%25D9%258A%25D8%25A7%25D8%25A...'
  },
  {
    id: 6,
    name: 'Perfumes',
    price: 5000,
    inStock: 4, 
    description: 'Very beautiful .',
    image: 'https://opf.sa/wp-content/uploads/2023/12/%D8%A3%D9%81%D8%B6%D9%84-%D8%A7%D9%84%D8%B9%D8%B7%D9%88%D8%B1-%D8%A7%D9%84%D9%86%D8%B3%D8%A7%D8%A6%D9%8A%D8%A9-.jpg'
  },
]);

const cart = ref([]);
const showProducts = ref(true);
const discount = ref(10);

const addToCart = (product) => {
  if (product.inStock > 0) {
    cart.value.push(product);
    product.inStock--;
  }
};

const totalPrice = computed(() => {
  const total = cart.value.reduce((sum, item) => sum + item.price, 0);
  return total - (total * discount.value) / 100;
});
</script>

<template>
  <div class="container mt-5">
    <Navbar :cart-count="cart.length" />

    <h1 class="my-4">My products</h1>

    <div class="row">
      <div v-for="product in products" :key="product.id" class="col-md-4 mb-4">
        <ProductCard :product="product" @add-to-cart="addToCart(product)" />
      </div>
    </div>
  </div>
</template>

<style>
@import 'https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css';
</style>

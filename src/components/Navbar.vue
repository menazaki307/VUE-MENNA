<script setup>
import { ref, computed, defineProps } from 'vue';

const props = defineProps({
  cartCount: {
    type: Number,
    required: true,
  },
});

const isCartEmpty = computed(() => props.cartCount === 0);

const searchQuery = ref(''); 

const handleSearch = () => {
  console.log('Searching for:', searchQuery.value);
};

</script>

<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-primary rounded-lg shadow-md">
    <div class="container-fluid">
      <!-- New Store Name -->
      <a class="navbar-brand text-white font-bold text-xl" href="#">Vue Shop</a>
      
      <!-- Toggler button for small devices -->
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse justify-content-end" id="navbarNav">
        <ul class="navbar-nav d-flex align-items-center">
          <!-- Search Bar -->
          <li class="nav-item me-3">
            <form class="d-flex" @submit.prevent="handleSearch">
              <input 
                class="form-control me-2 rounded-md" 
                type="search" 
                placeholder="Search products..." 
                aria-label="Search"
                v-model="searchQuery"
              >
              <button class="btn btn-outline-light rounded-md" type="submit">Search</button>
            </form>
          </li>
          
          <!-- Cart icon with product count -->
          <li class="nav-item">
            <a class="nav-link text-white position-relative" href="#">
              <!-- Shopping cart icon (you can replace it with a FontAwesome or SVG icon if you are using an icon library) -->
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" class="bi bi-cart3" viewBox="0 0 16 16">
                <path d="M0 1.5A.5.5 0 0 1 .5 1H2a.5.5 0 0 1 .485.379L2.89 3H14.5a.5.5 0 0 1 .49.598l-1 5a.5.5 0 0 1-.46.402H3.793a.5.5 0 0 1-.49-.402l-1-5A.5.5 0 0 1 2 3H.5a.5.5 0 0 1-.5-.5zM3.102 4l.84 4.474 8.675.249L14.102 4H3.102zM5 12a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm7 0a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm-7 1a1 1 0 1 1 0 2 1 1 0 0 1 0-2zm7 0a1 1 0 1 1 0 2 1 1 0 0 1 0-2z"/>
              </svg>
              <!-- Number of products in the cart -->
              <span v-if="!isCartEmpty" class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger">
                {{ cartCount }}
                <span class="visually-hidden">items in cart</span>
              </span>
            </a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  background-color: #5b42f3 !important; 
  padding: 1rem 1.5rem;
}

.navbar-brand {
  font-family: 'Inter', sans-serif; 
}

.bi-cart3 {
  color: white;
}

.btn-outline-light {
  border-color: #353030ff;
  color: #984f4fff;
}

.btn-outline-light:hover {
  background-color: #e96969ff;
  color: #855591ff;
}

.rounded-lg {
    border-radius: 0.5rem; 
}

.shadow-md {
    box-shadow: 0 4px 6px -1px rgba(53, 140, 195, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06); /* Light shadow */
}
</style>

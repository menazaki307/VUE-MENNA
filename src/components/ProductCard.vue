<script setup>
import { computed, defineProps, defineEmits } from 'vue';

const props = defineProps({
  product: {
    type: Object,
    required: true,
  },
});

const emits = defineEmits(['add-to-cart']);

const stockStatus = computed(() => {
  if (props.product.inStock > 2) {
    return 'in-stock';
  } else if (props.product.inStock > 0) {
    return 'low-stock';
  } else {
    return 'out-of-stock';
  }
});

const handleAddToCart = () => {
  emits('add-to-cart');
};
</script>

<template>
  <div class="card h-100">
    <img :src="product.image" class="card-img-top" :alt="product.name" />
    <div class="card-body d-flex flex-column">
      <h5 class="card-title">{{ product.name }}</h5>
      <p class="card-text">{{ product.description }}</p>
      <div class="mt-auto">
        <p class="h6 text-end">${{ product.price }}</p>
        
        <button
          @click="handleAddToCart"
          :disabled="stockStatus === 'out-of-stock'"
          class="btn btn-primary w-100 mt-2"
        >
          Add to card
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>

.card-img-top {
  height: 200px;
  object-fit: cover;
}
</style>
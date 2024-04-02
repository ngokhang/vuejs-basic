<script>
export default {
  name: "ProductItem",
  props: {
    product: {
      type: {
        id: Number,
        name: String,
        price: Number,
        quantity: Number,
      },
      required: true,
    },
  },
};
</script>

<template>
  <div class="info">
    <span>{{ product.name }} - </span> <span>{{ product.price }}</span> <span
    v-if="product.quantity > 0"> - {{ product.quantity }}</span>
  </div>
</template>

<style scoped>
.info {
  display: flex;
  gap: 10px;
}
</style>
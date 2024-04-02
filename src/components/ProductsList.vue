<script>
import ProductItem from "@/components/ProductItem.vue";

export default {
  name: "ProductsList",
  components: { ProductItem },
  data() {
    return {
      productsList: [
        {
          id: 1,
          name: "Product 1",
          price: 1000,
        },
        {
          id: 2,
          name: "Product 2",
          price: 2000,
        },
        {
          id: 3,
          name: "Product 3",
          price: 3000,
        },
      ],
      productsBought: [],
    };
  },
  methods: {
    buyProduct(product) {
      let productExisted = this.productsBought.find(p => p.id === product.id);
      if (productExisted) {
        productExisted.quantity += 1;
        return;
      }
      this.productsBought.push({ ...product, quantity: 1 });
    },
    removeProductBought(product) {
      this.productsBought = this.productsBought.filter(p => p.id !== product.id);
    },
    decreaseQuantity(product) {
      let productExisted = this.productsBought.find((p) => p.id === product.id);
      if (productExisted.quantity > 1) {
        productExisted.quantity -= 1;
        return;
      }
      this.productsBought = this.productsBought.filter((p) => p.id !== product.id);
    },
    formatCurrency(value) {
      return new Intl.NumberFormat("vi-VN", {
        style: "currency",
        currency: "VND",
      }).format(value);
    },
  },
  computed: {
    totalCost: function() {
      return this.productsBought.reduce((acc, curr) => acc + (curr.price * curr.quantity), 0);
    },
  },
  watch: {
    productsBought: {
      handler: function() {
        const test = this.productsBought.reduce((acc, curr) => acc + (curr.price * curr.quantity), 0);
        console.log(test);
      },
      deep: true,
    },
  },
};
</script>

<template>
  <div>
    <h2>Products List</h2>
    <ul class="products-list">
      <li v-for="product in productsList" :key="product.id" class="product-item">
        <ProductItem :product="product" @clickBuy="buyProduct" />
        <button class="btn-buy" @click="buyProduct(product)">Buy now!</button>
      </li>
    </ul>
  </div>

  <div>
    <h2>Products Bought</h2>
    <ul class="products-list bought">
      <li v-for="product in productsBought" :key="product.id" class="product-item">
        <ProductItem :product="product" />
        <button class="btn-increase" @click="buyProduct(product)">Increase</button>
        <button class="btn-decrease" @click="decreaseQuantity(product)">Decrease</button>
        <button class="btn-remove" @click="removeProductBought(product)">Remove</button>
      </li>
    </ul>
    <hr>
    <div>
      <span>Total Cost: {{ formatCurrency(totalCost) }}</span>
    </div>
  </div>
</template>

<style scoped>
.products-list {
  max-height: 200px;
  overflow-y: auto;
}

.product-item {
  display: flex;
  gap: 10px;
  margin: 10px 0;
}
</style>
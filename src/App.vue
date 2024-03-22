<template>
  <div id="app" class="container">
    <div class="left">
      <ProductList :products="products" @add-to-cart="addToCart" class="product-list" />
    </div>
    <div class="right">
      <ShoppingCart :cart="cart" @update-quantity="updateQuantity" @remove-item="removeItem" />
    </div>
  </div>
</template>

<script>
import ProductList from './components/ProductList.vue';
import ShoppingCart from './components/ShoppingCart.vue';

export default {
  name: 'App',
  components: {
    ProductList,
    ShoppingCart
  },
  data() {
    return {
      products: [
        { id: 1, name: 'Plain Tshirt', price: 10 },
        { id: 2, name: 'Sweater Jacket', price: 20 },
        { id: 3, name: 'Wide Leg Pants', price: 50 },
        { id: 4, name: 'Cargo Pants', price: 100 },
      ],
      cart: []
    };
  },
  methods: {
    addToCart(product) {
      const existingItem = this.cart.find(item => item.id === product.id);
      if (existingItem) {
        existingItem.quantity++;
      } else {
        this.cart.push({ ...product, quantity: 1 });
      }
    },
    updateQuantity(itemId, newQuantity) {
      const item = this.cart.find(item => item.id === itemId);
      if (item) {
        item.quantity = newQuantity;
      }
    },
    removeItem(itemId) {
      this.cart = this.cart.filter(item => item.id !== itemId);
    }
  }
};
</script>

<style>
.center-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.container {
  display: flex;
}

.left {
  margin-right: 20px;
}

.right {
  margin-left: auto; 
}

</style>
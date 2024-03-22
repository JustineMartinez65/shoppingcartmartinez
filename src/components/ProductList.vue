<template>
  <div>
    <h2>Products</h2>
    <ul>
      <li v-for="product in products" :key="product.id">
        <span>{{ product.name }} - ${{ product.price }}</span>
        <button @click="addToCart(product)">Add to Cart</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'ProductList',
  props: {
    products: {
      type: Array,
      required: true
    }
  },
  methods: {
    addToCart(product) {
      this.$emit('add-to-cart', product);
    }
  }
};
</script>

<style scoped>
.product-list {
  background-color: #421313; 
  padding: 20px; 
}
h2 {
  color: #ffffff;
  font-weight: bold; 
  font-family: 'Times New Roman', Times, serif;
  text-align: center;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  margin-bottom: 10px;
  display: flex;
  align-items: center; 
}

.product-name {
margin-right: 10px; 
}

button {
  background-color: #007bff;
  color: #fff;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
  margin-left: auto; 
  white-space: nowrap;
}

button:hover {
  background-color: #0056b3;
}
</style>
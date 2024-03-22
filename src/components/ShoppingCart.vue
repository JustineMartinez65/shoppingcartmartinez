<template>
  <div class="shopping-cart">
    <h2>Shopping Cart</h2>
    <ul>
      <li v-for="item in cart" :key="item.id">
        <span>{{ item.name }} </span> 
        <span>Quantity:</span>
        <input type="number" v-model="item.quantity" @input="updateQuantity(item.id, $event.target.value)">
        <button @click="removeItem(item.id)">Remove</button>
      </li>
    </ul>
    <p>Total: ${{ total }}</p>
  </div>
</template>

<script>
export default {
  name: 'ShoppingCart',
  props: {
    cart: {
      type: Array,
      required: true
    }
  },
  computed: {
    total() {
      return this.cart.reduce((total, item) => total + (item.price * item.quantity), 0);
    }
  },
  methods: {
    updateQuantity(itemId, newQuantity) {
      this.$emit('update-quantity', itemId, newQuantity);
    },
    removeItem(itemId) {
      this.$emit('remove-item', itemId);
    }
  }
};
</script>

<style scoped>
.shopping-cart {
  margin-left: auto; 
  max-width: 300px; 
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

span {
  margin-right: 10px;
}

input {
  width: 50px;
}

button {
  background-color: #dc3545;
  color: #fff;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
}

button:hover {
  background-color: #c82333;
}

p {
  font-weight: bold;
}
</style>

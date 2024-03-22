<template>
  <div id="app">
    <h1 class="name" >FROZEN GOODS ONLINE SHOP</h1>
    <div class="container">
      <ProductListing @add-to-cart="addToCart" class="left-panel"></ProductListing>
      <ShoppingCart :cart="cart" @update-quantity="updateQuantity" @remove-from-cart="removeFromCart" class="right-panel"></ShoppingCart>
    </div>
  </div>
</template>

<script>
import ProductListing from './components/ProductListing.vue';
import ShoppingCart from './components/ShoppingCart.vue';

export default {
  components: {
    ProductListing,
    ShoppingCart
  },
  data() {
    return {
      cart: []
    };
  },
  methods: {
    addToCart(item) {
      const existingItemIndex = this.cart.findIndex(i => i.name === item.name);
      if (existingItemIndex !== -1) {
        this.cart[existingItemIndex].quantity++;
      } else {
        this.cart.push({ ...item, quantity: 1 });
      }
    },
    removeFromCart(index) {
      this.cart.splice(index, 1);
    },
    updateQuantity({ index, quantity }) {
      this.cart[index].quantity = quantity;
      if (this.cart[index].quantity <= 0) {
        this.cart.splice(index, 1);
      }
    }
  }
};
</script>

<style>
body{
  font-family: 'Arial', sans-serif;
}
.name{
  text-align: center;
}
.container {
  display: flex;
}

.left-panel {
  flex: 1;
}

.right-panel {
  flex: 1;
}
</style>

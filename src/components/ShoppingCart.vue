<template>
  <div class="cart">
    <h2>SHOPPING CART</h2>
    <!-- Cart items -->
    <div v-for="(item, index) in cart" :key="index" class="cart-item">
      <div class="item-details">
        <p class="item-name">{{ item.name }}</p>
        <p class="item-price">₱ {{ item.price }}</p>
        <div class="item-quantity-controls">
          <button @click="decrementQuantity(index)">-</button>
          <span class="item-quantity">{{ item.quantity }}</span>
          <button @click="incrementQuantity(index)">+</button>
        </div>
      </div>
      <div class="quantity-controls">
        <button @click="removeFromCart(index)">Remove</button>
      </div>
    </div>

    <!-- Total -->
    <p class="total">Total: ₱ {{ total }}</p>
  </div>
</template>

<script>
export default {
  props: {
    cart: {
      type: Array,
      default: () => [],
    },
  },
  computed: {
    total() {
      if (this.cart.length === 0) {
        return 0; // Return 0 if the cart is empty
      }
      return this.cart.reduce((acc, item) => acc + item.price * item.quantity, 0);
    },
  },
  methods: {
    decrementQuantity(index) {
      if (this.cart[index].quantity > 1) {
        // Emit an event to update the quantity
        this.$emit('update-quantity', { index, quantity: this.cart[index].quantity - 1 });
      }
    },
    incrementQuantity(index) {
      // Emit an event to update the quantity
      this.$emit('update-quantity', { index, quantity: this.cart[index].quantity + 1 });
    },
    removeFromCart(index) {
      // Ask for confirmation before removing the item
      const confirmRemove = confirm("Are you sure you want to remove this item from your cart?");
      if (confirmRemove) {
        // Emit an event to remove the item from the cart
        this.$emit('remove-from-cart', index);
      }
    },
  },
};
</script>

<style scoped>
body{
  font-family: 'Arial', sans-serif;
}
h2{
  text-align: center;
}
.cart {
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  width: 15px;
  float: right;
  margin-right: 20px;
}

.cart-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
  border-bottom: 1px solid #ddd;
  padding-bottom: 10px;
}

.item-details {
  flex: 1;
}

.item-name {
  font-weight: bold;
}

.item-price {
  margin-left: 10px;
}

.item-quantity-controls {
  display: flex;
  align-items: center;
}

.item-quantity {
  margin: 0 5px;
}

.quantity-controls button {
  background-color: #f44336;
  color: white;
  border: none;
  border-radius: 3px;
  padding: 5px 10px;
  cursor: pointer;
}

.quantity-controls button:hover {
  background-color: #d32f2f;
}

.total {
  font-weight: bold;
  margin-top: 10px;
}
</style>

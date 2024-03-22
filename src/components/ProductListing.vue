<template>
  <div class="product-list">
    <h2>PRODUCTS</h2>
    <ul>
      <li v-for="product in products" :key="product.id" class="product-item">
        <div class="product-info">
          <span class="product-name">{{ product.name }}</span>
          <span class="product-price">₱{{ product.price }}</span>
        </div>
        <button @click="addToCart(product)" class="add-to-cart-btn">Add to Cart</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [
        { id: 1, name: 'Longganisa', price: 30 },
        { id: 2, name: 'Sinless', price: 30 },
        { id: 3, name: 'TJ Hotdog Jumbo', price: 14 },
        { id: 4, name: 'Embutido', price: 15 },
        { id: 5, name: 'Siomai', price: 50 },
        { id: 6, name: 'Boneless Bangus', price: 50 },
        { id: 7, name: 'Sweet Ham', price: 65 },
        { id: 8, name: 'Tocino', price: 67 },
        { id: 9, name: 'Bacon', price: 95 },
        { id: 10, name: 'Lumpiang Shanghai', price: 89 }
      ]
    };
  },
  methods: {
    addToCart(item) {
      this.$emit('add-to-cart', item);
    }
  }
};
</script>

<style scoped>
body{
  font-family: 'Arial', sans-serif;
}
h2 {
  text-align: center;
}

.product-list {
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  width: 15%;
  float: right;
  margin-right: 20px;
}

.product-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
}

.product-info {
  flex: 1;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.product-name {
  font-weight: bold;
}

.product-price {
  margin-left: 10px;
}

.add-to-cart-btn {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  margin-left: 20px;
}

.add-to-cart-btn:hover {
  background-color: #45a049;
}
</style>

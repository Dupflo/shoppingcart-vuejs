<template>
  <div>
    <div>
      <ul>
        <li :key="product.id" v-for="product in products" class="price-row">
          <div>{{ product.name }}</div>
          <div class="quantity-row">
            <div class="price-quantity">Qty: {{ product.qty }}</div>
            <div>{{ formatMoney(product.price * product.qty) }}</div>
          </div>
        </li>
      </ul>
    </div>

    <div class="price-row">
      <div class="price-label">Sub-total</div>
      <div class="price-wrapper">{{ formatMoney(subtotal) }}</div>
    </div>
    <div class="price-row">
      <div class="price-label">Shipping</div>
      <div class="price-wrapper">{{ formatMoney(shipping) }}</div>
    </div>
    <div class="price-row">
      <div class="price-label">Total</div>
      <div class="price-wrapper">{{ formatMoney(subtotal + shipping) }}</div>
    </div>
    <button class="checkout-button">CHECKOUT</button>
  </div>
</template>

<script>
import { bus } from "../bus";

export default {
  data: function() {
    bus.$on("add-product", product => {
      this.addProduct(product);
    });
    return {
      products: []
    };
  },
  computed: {
    subtotal: function() {
      let subtotal = 0;
      this.products.forEach(product => {
        subtotal += product.price * product.qty;
      });
      return subtotal;
    },
    shipping: function() {
      let totalQuantity = 0;
      this.products.forEach(product => {
        totalQuantity += product.qty;
      });
      return totalQuantity * 399;
    }
  },
  methods: {
    addProduct: function(product) {
      let productIndex = this.products.findIndex(function(currentProduct) {
        return currentProduct.id === product.id;
      });
      if (productIndex >= 0) {
        return this.products[productIndex].qty++;
      }
      this.products.push({ ...product, qty: 1 });
    },
    formatMoney: function(cents) {
      return "$" + cents / 100;
    }
  }
};
</script>

<style scoped>
.quantity-row {
  display: flex;
}
.price-quantity {
  margin-right: 15px;
}
.checkout-button {
  width: 100%;
  text-align: center;
  padding: 10px 0;
  background: #000;
  color: #eee;
}
.price-row {
  display: flex;
  justify-content: space-between;
  border-bottom: 1px solid #eee;
  margin: 10px;
  padding-bottom: 10px;
}
</style>

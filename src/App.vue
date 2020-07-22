<template>
  <div id="app">
    <h1>The Cup Store</h1>

    <product v-for="product in products" :key="product.id" :product="product" />

    <Cart></Cart>
  </div>
</template>

<script>
import Product from "./components/Product";
import Cart from "./components/Cart";
import "./assets/styles.css";

export default {
  name: "App",
  data() {
    return {
      products: [
        {
          id: 120,
          name: "Colorful Cups",
          price: 999,
          image: require("./assets/images/cups1.jpg"),
        },
        {
          id: 121,
          name: "Coffee & Home",
          price: 1499,
          image: require("./assets/images/cups2.jpg"),
        },
        {
          id: 123,
          name: "Old Red Friend",
          price: 1999,
          image: require("./assets/images/cups3.jpg"),
        },
      ],
    };
  },
  components: {
    Product,
    Cart,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

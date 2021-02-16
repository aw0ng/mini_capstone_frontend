<template>
  <div class="products-index">
    <h1>All Products</h1>
    <div v-for="product in products" v-bind:key="product.id">
      <h2>{{ product.name }}</h2>
      <img v-bind:src="product.primary_image_url" v-bind:alt="product.name" />
      <p>
        <router-link v-bind:to="`/products/${product.id}`">More info</router-link>
      </p>
    </div>
  </div>
</template>

<style>
img {
  width: 50%;
  height: auto;
}
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      products: [],
    };
  },
  created: function() {
    axios.get("/api/products").then(response => {
      console.log("products index", response);
      this.products = response.data;
    });
  },
  methods: {},
};
</script>

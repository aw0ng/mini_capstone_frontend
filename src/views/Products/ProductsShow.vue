<template>
  <div class="products-show">
    <h2>{{ product.name }}</h2>
    <p>{{ product.description }}</p>
    <p>{{ product.price }}</p>
    <img v-bind:src="product.primary_image_url" v-bind:alt="product.name" />
    <p>
      <router-link v-bind:to="`/products/${product.id}/edit`">Edit Product</router-link>
    </p>
    <p>
      <router-link to="/products">Back to all products</router-link>
    </p>
  </div>
</template>

<style>
img: {
  width: 40%;
  height: auto;
}
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      product: {},
    };
  },
  created: function() {
    axios.get("/api/products/" + this.$route.params.id).then(response => {
      console.log("products show", response);
      this.product = response.data;
    });
  },
  methods: {},
};
</script>

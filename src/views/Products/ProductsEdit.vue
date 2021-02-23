<template>
  <div class="products-edit">
    <h1>Edit Product</h1>
    <form v-on:submit.prevent="updateProduct(product)">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Name:
      <input type="text" v-model="product.name" />
      Price:
      <input type="text" v-model="product.price" />
      Description:
      <input type="text" v-model="product.description" />
      Supplier:
      <input type="text" v-model="product.supplier" />
      Image Url:
      <input type="text" v-model="product.primary_image_url" />
      <input type="submit" value="Update" />
    </form>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      product: {},
      errors: [],
    };
  },
  created: function() {
    axios.get("/api/products/" + this.$route.params.id).then(response => {
      console.log("products show", response);
      this.product = response.data;
    });
  },
  methods: {
    updateProduct: function(product) {
      var params = {
        name: product.name,
        price: product.price,
        description: product.description,
        supplier: product.supplier,
        imageurl: product.primary_image_url,
      };
      axios
        .patch("/api/products/" + product.id, params)
        .then(response => {
          console.log("products update", response);
          this.$router.push("/products");
        })
        .catch(error => {
          console.log("products udpate error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

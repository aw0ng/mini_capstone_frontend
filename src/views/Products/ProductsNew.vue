<template>
  <div class="products-new">
    <h1>New Product</h1>
    <form v-on:submit.prevent="createProduct()">
      <ul>
        <li :v-for="error in errors">{{ error }}</li>
      </ul>
      <a href="/login">Login</a>
      Name:
      <input type="text" v-model="newProductName" />
      Price:
      <input type="text" v-model="newProductPrice" />
      Description:
      <input type="text" v-model="newProductDescription" />
      Supplier:
      <input type="text" v-model="newProductSupplier" />
      Image Url:
      <input type="text" v-model="newProductImage" />
      <input type="submit" value="Create" />
    </form>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      newProductName: "",
      newProductPrice: "",
      newProductDescription: "",
      newProductSupplier: "",
      newProductImage: "",
      errors: [],
    };
  },
  created: function() {},
  methods: {
    createProduct: function() {
      var params = {
        name: this.newProductName,
        price: this.newProductPrice,
        description: this.newProductDescription,
        supplier: this.newProductSupplier,
        primary_image_url: this.newProductImage,
      };
      axios
        .post("/api/products", params)
        .then(response => {
          console.log("products create", response);
          this.$router.push("/products");
        })
        .catch(error => {
          console.log("products create error", error.response);
          this.erorrs = error.response.data.errors;
        });
    },
  },
};
</script>

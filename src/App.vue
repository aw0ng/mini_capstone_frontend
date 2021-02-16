<template>
  <div id="app">
    <div id="nav">
      <router-link to="/signup">Signup</router-link>
      |
      <router-link to="/login">Login</router-link>
      |
      <router-link to="/products">All Products</router-link>
      |
      <router-link to="/products/new">New Product</router-link>
      |
      <router-link to="/logout">Logout</router-link>
      |
    </div>
    <router-view />
  </div>
</template>

<style></style>

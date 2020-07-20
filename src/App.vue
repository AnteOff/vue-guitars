<template>
  <div id="app">
    <NavBar :cart="cart" :premium="premium" @log-out="logout" @log-in="login"/>
    <Products :premium="premium" @add-to-cart="updateCart" @remove-from-cart="removeCart"/>
  </div>
</template>

<script>
import NavBar from '@/components/NavBar.vue';
import Products from '@/components/Products.vue';

export default {
  name: "App",
  components: {
    NavBar,
    Products
  },
  data() {
    return {
      premium: true,
      cart:[]
    }
  },
  methods: {
    updateCart(productID) {
      this.cart.push(productID)
    },
    removeCart(productID) {
      for(let i = this.cart.length - 1; i >= 0; i--) {
        if (productID === this.cart[i]) {
          this.cart.splice(i,1)
        }
      }
    },
    logout(setFalse) {
      this.premium = setFalse
    },
    login(setTrue) {
      this.premium = setTrue
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

body {
  margin: 0px;
}
</style>

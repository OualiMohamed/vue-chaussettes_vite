<script>
import ProductDisplay from '../components/ProductDisplay.vue'

export default {
  name: 'HomeView',
  components: {
    ProductDisplay,
  },
  data() {
    return {
      cart: [],
      premium: true,
    }
  },
  methods: {
    updateCart(id) {
      this.cart.push(id)
    },
    removeById(id) {
      // this.cart--;
      const index = this.cart.indexOf(id)
      if (index > -1) {
        this.cart.splice(index, 1)
      }
    },
  },
}
</script>

<template>
  <main>
    <div class="cart">Cart({{ cart.length }})</div>
    <ProductDisplay :premium="premium" @add-to-cart="updateCart" @remove-from-cart="removeById" />
  </main>
</template>

<style>
.nav-bar {
  background: linear-gradient(-90deg, #84cf6a, #16c0b0);
  width: 100%;
  height: 60px;
  margin-bottom: 25px;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.57);
}

.cart {
  margin: 25px 100px;
  float: right;
  border: 1px solid #d8d8d8;
  padding: 10px 30px;
  background-color: white;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);
}
</style>

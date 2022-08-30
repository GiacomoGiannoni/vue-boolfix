<template>
  <div id="app">
    <MyHeader @fetch-products="showProducts" />
    <main>
      <MyProducts :products="products" :isLoading="isLoading" />
    </main>
  </div>
</template>

<script>
import MyHeader from './components/MyHeader'
import MyProducts from './components/MyProducts.vue'
export default {
  name: 'App',
  components: {
    MyHeader,
    MyProducts
  },
  data() {
    return {
      isLoading: false,
      products: [],
    };
  },
  methods: {
    showProducts(products) {
      this.products = products;
      console.log(this.products);
    }
  }
}
</script>

<style lang="scss">
  @import '~@fortawesome/fontawesome-free/css/all.css';

</style>

<template>
  <div id="app">
    <MyHeader />
    <main>
      <MyProducts />
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
  }
}
</script>

<style lang="scss">
  @import '~@fortawesome/fontawesome-free/css/all.css';

#app {
  
}
</style>

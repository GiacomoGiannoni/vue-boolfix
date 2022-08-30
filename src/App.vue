<template>
  <div id="app">
    <MyHeader />
    <main>
      <MyProducts />
    </main>
  </div>
</template>

<script>
import axios from "axios";
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
      products: [],
      query:"2001",
      api_key: "e6be65eb29366a9451fa37857751b276",
      url: "https://api.themoviedb.org/3",
    };
  },
  methods: {
    getMyProducts(url) {
      const config = {
        params: {
          api_key: this.api_key,
					query: this.query,
					language: "it-IT",
        },
      };
      axios
      .get(`${url}/search/movie?`, config).then((res) => {
        this.products = res.data.results;
        console.log(this.products);
      });
    }
  },
  mounted() {
		this.getMyProducts(this.url);
	},
}
</script>

<style lang="scss">
  @import '~@fortawesome/fontawesome-free/css/all.css';

#app {
  
}
</style>

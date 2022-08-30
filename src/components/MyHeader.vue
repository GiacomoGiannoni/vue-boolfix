<template>
    <div>
        <input v-model="search" type="text" @keyup.enter="getProducts(url)" placeholder="Cerca un film"/>
        <button type="button" @click="getProducts(url)">Search</button>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: "MyHeader",
    props: ['products'],
    data () {
        return {
            search: '',
            query: "2001",
            api_key: "e6be65eb29366a9451fa37857751b276",
            url: "https://api.themoviedb.org/3",
        };
    },
    methods: {
        getProducts(url) {
            const config = {
                params: {
                    api_key: this.api_key,
                    query: this.search,
                    language: "it-IT",
                },
            };
            this.isLoading = true;
            axios
            .get(`${url}/search/movie?`, config).then((res) => {
				this.$emit('fetch-products', res.data.results);
				this.isLoading = false;
			});
        },
    },
};
</script>

<style>

</style>
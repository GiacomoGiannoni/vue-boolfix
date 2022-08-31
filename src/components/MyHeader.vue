<template>
    <header class="row m-0">
        <div class="col d-flex justify-content-between align-items-center px-4">
            <div>
                <h1>BOOLFLIX</h1>
            </div>
            <div class="d-flex">
                <input
                class="form-control" 
                v-model="search"
                type="text" 
                @keyup.enter="getProducts()" 
                :placeholder="placeholder || 'Cerca qualcosa...'"
                />
                <button class="ms-2 btn btn-danger" type="button" @click="getProducts()">Search</button>

            </div>
        </div>

    </header>
</template>

<script>
import axios from 'axios';

export default {
    name: "MyHeader",
    props: ["placeholder"],
    data () {
        return {
            search: "",
            query: "2001",
            api_key: "e6be65eb29366a9451fa37857751b276",
            url: "https://api.themoviedb.org/3",
        };
    },
    methods: {
        fetchApi(endpoint, config, target) {
            axios
            .get(`${this.url}/${endpoint}`, config)
            .then((res) => {
                this.$emit(`fetch-${target}`, res.data.results, target);
            })
            .catch((err) => {
                console.log(err);
            });
        },
        getProducts() {
            const config = {
                params: {
                    api_key: this.api_key,
                    query: this.search,
                    language: "it-IT",
                },
            };
            this.fetchApi("search/movie", config, "products");
            this.fetchApi("search/tv", config, "series");
            this.search = '';
		},
    },
};
</script>

<style lang="scss" scoped>
    
header {
	background-color: rgb(27, 27, 27);
	height: 100px;

	h1 {
		color: rgb(194, 0, 0);
	}
}
</style>
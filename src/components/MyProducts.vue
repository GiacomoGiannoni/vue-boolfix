<template>
	<div>
        <MyLoader v-if="isLoading"/>
        <ul>
            <li v-for="product in products" :key="product.id">
                <h3>
                    Titolo: {{product.title}} <br>
                    Titolo originale: {{product.orginal_title}}
                </h3>
                <p>
                    Lingua: {{product.original_language}} <br>
                    Voto: {{product.vote_average}}
                </p>
            </li>
        </ul>
    </div>
</template>

<script>
import MyLoader from "./MyLoader";

export default {
	name: "MyProducts",
    components: {
    MyLoader,
},
    props: ["products", "isLoading"],
};
</script>

<style>

</style>
<template>
    <div>
        <ul class="list-unstyled d-flex flex-column" :style="bgStyle">
            <li><strong>Titolo:</strong> {{item.title || item.name}}</li>
            <li><strong>Titolo originale:</strong> {{item.original_title || item.original_name}}</li>
            <li class="language">
                Lingua:
                <img v-if="countries.includes(item.original_language)" :src="setFlag" :alt="item.title" />
                <span v-else>{{ item.original_language.toUpperCase()}}</span>
            </li>
            <li id="stars">
                <i v-for="i in 5" :key="i" class="fa-star" :class="i <= setStar ? 'fa-solid' : 'fa-regular'"></i>
            </li>
            <li>{{item.overview || "Nessuna descrizione disponibile"}}</li>
        </ul>
    </div>
</template>

<script>

export default {
	name: "MyMain",
    components: {},
    props:["item"],
    data() {
        return {
            countries: ["it", "en", "es", "fr", "us" ],
            baseUri: "http://image.tmdb.org/t/p/w342",
            vote: this.item.vote_average,
        };
    },
    computed: {
        setFlag() {
			return require(`@/assets/img/${this.item.original_language}.png`);
		},
        setPoster() {
			let imgPath = `${this.baseUri}${this.item.poster_path}`;
			return imgPath;
		},
        setAlternativePoster() {
			return require(`@/assets/img/no-image.png`);
		},
        setStar() {
			let stars = Math.ceil(this.vote / 2);
			return stars;
		},
        bgImage() {
			return this.item.poster_path ? this.setPoster : this.setAlternativePoster;
		},
		bgStyle() {
			return {
				backgroundImage: `url(${this.bgImage})`,
			};
		},
    },
};
</script>

<style lang="scss" scoped>
@import '@/style/vars.scss';
    .fa-star {
        color: rgb(236, 201, 41);
    }
    
    .language img {
        height: auto;
        width: 40px;
    }

    ul {
        background-repeat: no-repeat;
        background-position: center;
        background-size: cover;
        height: 450px;
        width: 300px;
        border-radius: 5px;
        overflow-y: scroll;
        border: 1px solid white;
    }

    li {
        display: none;
    }

    ul:hover li {
	    display: inline;
        margin: 10px;
    }

    ul:hover {
        background-image: none !important;
        background-color: $color-main;
    }
</style>
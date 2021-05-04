<template>
    <div class="results">
        <h3>{{ searchTerm }}</h3>
        <button class="button" v-on:click="reDraw">Redraw</button>
        <Loading v-if="loading" />
        <Error v-else-if="error" :error="error" />
        <div v-else-if="images.length === 0">No results</div>
        <div
            v-masonry
            transition-duration="3s"
            fit-width="true"
            item-selector=".item"
            class="masonry-container"
            v-else
        >
            <div
                v-masonry-tile
                class="item"
                v-for="image in images"
                :key="image.id"
            >
                <ImageCard :image="image" />
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import Loading from "./Loading.vue";
import Error from "./Error.vue";
import { GalleryModel } from "../models/gallery";
import ImageCard from "./ImageCard.vue";
import { VueMasonryPlugin } from "vue-masonry";
import Vue from "vue";
import axios from "axios";

Vue.use(VueMasonryPlugin);

export default Vue.extend({
    name: "ImageGrid",
    props: {
        searchTerm: String,
    },
    data: function() {
        return {
            images: new Array<GalleryModel>(),
            loading: true,
            error: "",
        };
    },
    components: {
        ImageCard,
        Loading,
        Error,
    },
    watch: {
        searchTerm() {
            this.fetchImages();
        },
    },
    methods: {
        fetchImages() {
            this.loading = true;
            const query = this.searchTerm;
            const sort = "time";
            const page = 1;
            const win = "all";
            // const showViral = true;
            const showMature = true;
            // const albumPreviews = true;
            const url = `https://api.imgur.com/3/gallery/search/${sort}/${win}/${page}?mature=${showMature}&q=${query}`;
            axios
                .get(url, {
                    headers: {
                        Authorization: "client-id 8f89bca31953552",
                    },
                })
                .then((res) => {
                    this.loading = false;
                    this.images = res.data.data as GalleryModel[];
                    this.reDraw();
                })
                .catch((error) => {
                    this.loading = false;
                    this.error = error.toString();
                });
        },
        reDraw: function() {
            this.$redrawVueMasonry();
        },
    },
    created() {
        this.fetchImages();
    },
});
</script>

<style scoped>
.results {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.masonry-container {
    background-color: #fafafa;
    width: 80%;
}

.item {
    margin: 1rem;
    border-radius: 0.5rem;
    background-color: white;
    max-height: 300px;
    max-width: 300px;
}

.button {
    padding: 0.5rem 1rem;
    border-radius: 0.2rem;
    border: none;
    box-shadow: 2px 2px #0b414121;
    background-color: #0cc2c2;
    color: white;
    text-transform: uppercase;
}
</style>

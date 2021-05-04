<template>
    <div>
        <button class="button" @click="prev" v-if="hasPrev">&#8592;</button>
        <button class="button" @click="next" v-if="hasNext">&#8594;</button>
        <a :href="image.link">
            <VideoElement
                :video="image.images[currentImage]"
                v-if="image.images[currentImage].type === 'video/mp4'"
            />
            <SingleImage :image="image.images[currentImage]" v-else />
        </a>
    </div>
</template>

<script lang="ts">
import Vue from "vue";
import { ImageAlbumModel } from "../models/imageAlbum";
import VideoElement from "../components/Video.vue";
import SingleImage from "../components/SingleImage.vue";

export default Vue.extend({
    data() {
        return {
            currentImage: 0,
        };
    },
    props: {
        image: Object as () => ImageAlbumModel,
    },
    methods: {
        prev() {
            this.currentImage--;
        },
        next() {
            this.currentImage++;
        },
    },
    computed: {
        hasNext() {
            return this.currentImage < this.image.images.length - 1;
        },
        hasPrev() {
            return this.currentImage > 0;
        },
    },
    components: {
        VideoElement,
        SingleImage,
    },
});
</script>

<style scoped>
.button {
    border-radius: 0.2rem;
    border: none;
    box-shadow: 2px 2px #0b414121;
    background-color: #0cc2c2;
    color: white;
    text-transform: uppercase;
}
</style>

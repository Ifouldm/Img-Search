<template>
    <div class="card">
        <div class="title">{{ image.title }}</div>
        <ImageAlbum :image="image" v-if="image.is_album" />
        <Video :video="image" v-else-if="image.type === 'video/mp4'" />
        <SingleImage
            :image="image"
            v-else-if="
                ['image/png', 'image/jpeg', 'image/jpg', 'image/gif'].includes(
                    image.type
                )
            "
        />
        <span v-else>NO OUTPUT</span>
    </div>
</template>

<script lang="ts">
import Vue from "vue";
import Video from "../components/Video.vue";
import ImageAlbum from "../components/ImageAlbum.vue";
import SingleImage from "../components/SingleImage.vue";

export default Vue.extend({
    name: "ImageCard",
    props: {
        image: {},
    },
    components: {
        Video,
        ImageAlbum,
        SingleImage,
    },
});
</script>

<style>
.card {
    padding: 1rem;
    box-shadow: 0px 2px 1px -1px rgba(0, 0, 0, 0.2),
        0px 1px 1px 0px rgba(0, 0, 0, 0.14), 0px 1px 3px 0px rgba(0, 0, 0, 0.12);
}

a {
    text-decoration: none;
}

.title {
    margin-bottom: 1rem;
    text-align: center;
    text-decoration: underline;
    background-color: white;
    color: black;
}
</style>

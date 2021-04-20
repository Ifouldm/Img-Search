<template>
    <div class="group">
        <div class="image" v-for="image in images" :key="image.id">
            {{ image.title }}
            <video
                width="320"
                height="240"
                controls
                v-if="image.type === 'video/mp4'"
            >
                <source :src="image.link" type="video/mp4" />
                Your browser does not support the video tag.
            </video>
            <img
                :src="image.link"
                :alt="image.id"
                v-else-if="
                    image.type ===
                        ['image/png', 'image/jpeg', 'image/jpg'].includes(
                            image.type
                        )
                "
            />
            <span v-else>{{ image.type }}</span>
        </div>
    </div>
</template>

<script>
import axios from "axios";
export default {
    name: "Gallery",
    data: function() {
        return {
            images: [],
        };
    },
    methods: {
        fetchImages() {
            const subreddit = "aww";
            const sort = "time";
            const page = 1;
            const showViral = true;
            const showMature = true;
            const albumPreviews = true;
            const url = `https://api.imgur.com/3/gallery/r/${subreddit}/${sort}/${page}?showViral=${showViral}&mature=${showMature}&album_previews=${albumPreviews}`;
            axios
                .get(url, {
                    headers: {
                        Authorization: "client-id 8f89bca31953552",
                    },
                })
                .then((res) => {
                    this.images = res.data.data;
                    console.log(this.images);
                })
                .catch((error) => console.log(error));
        },
    },
    mounted() {
        this.fetchImages();
    },
};
</script>

<style>
.group {
    display: flex;
    flex-direction: column;
}
.image {
    max-width: 50%;
    max-height: 50%;
}
</style>

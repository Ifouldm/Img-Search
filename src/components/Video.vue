<template>
    <video width="100%" controls>
        <source :src="video.link" type="video/mp4" />
        Your browser does not support the video tag.
    </video>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
    name: "VideoElement",
    props: {
        video: {},
    },
});
</script>

<style></style>

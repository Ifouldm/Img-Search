<template>
    <a :href="image.link">
        <img :src="image.link" :alt="image.id" width="100%" />
    </a>
</template>

<script>
import Vue from "vue";

export default Vue.extend({
    props: {
        image: {},
    },
});
</script>

<style></style>

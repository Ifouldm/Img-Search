<template>
    <div id="app">
        <Gallery />
    </div>
</template>

<script lang="ts">
import Vue from "vue";
import Gallery from "./components/Gallery.vue";

export default Vue.extend({
    name: "App",
    components: {
        Gallery,
    },
});
</script>

<style>
#app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
}
</style>

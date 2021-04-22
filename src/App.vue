<template>
    <div id="app">
        <Selector @searchTerm="changeSubreddit" />
        <ImageGrid :searchTerm="searchTerm" />
    </div>
</template>

<script lang="ts">
import Vue from "vue";
import ImageGrid from "./components/ImageGrid.vue";
import Selector from "./components/Selector.vue";

export default Vue.extend({
    name: "App",
    data() {
        return {
            searchTerm: "aww",
        };
    },
    components: {
        ImageGrid,
        Selector,
    },
    methods: {
        changeSubreddit(searchTerm) {
            this.searchTerm = searchTerm;
        },
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
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
</style>

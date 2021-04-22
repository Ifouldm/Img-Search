<template>
    <form class="searchbar" @submit.prevent="search">
        <div class="textfield">
            <input
                id="searchField"
                type="text"
                v-model="searchTerm"
                @submit="search"
            />
        </div>
        <button class="button" @click="search">Search</button>
    </form>
</template>

<script>
import Vue from "vue";

export default Vue.extend({
    data() {
        return {
            searchTerm: "",
        };
    },
    methods: {
        search() {
            this.$emit("searchTerm", this.searchTerm);
        },
    },
});
</script>

<style scoped>
.searchbar {
    padding: 1rem;
}

.textfield {
    display: inline;
    position: relative;
    margin: 0 1rem;
}

.textfield::after {
    position: absolute;
    content: "Search Term";
    color: #8a8a8a;
    font-size: 0.8rem;
    top: -1.5rem;
    left: 10px;
}

.textfield input {
    padding: 1rem;
    background-color: #f5f5f5;
    border-radius: 0.2rem 0.2rem 0 0;
    outline: none;
    border: none;
    border-bottom: 1px solid black;
}

.textfield input:focus {
    border-bottom: 2px solid #0b4141;
}

.button {
    padding: 1rem 1.5rem;
    border-radius: 0.2rem;
    border: none;
    box-shadow: 2px 2px #0b414121;
    background-color: #0cc2c2;
    color: white;
    text-transform: uppercase;
}
</style>

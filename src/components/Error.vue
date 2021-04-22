<template>
    <div class="error">Error: {{ error }}</div>
</template>

<script lang="ts">
export default {
    props: {
        error: String,
    },
};
</script>

<style>
.error {
    font-size: 3rem;
}
</style>

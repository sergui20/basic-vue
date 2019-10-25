<template>
    <div>
        <li v-bind:key="artist.name">
            <h2><a v-bind:href="artist.url" target="_blank">{{ artist.name }}</a></h2>
            <img v-bind:src="artist.image[2]['#text']">
        </li>    
    </div>
</template>

<script>
    export default {
        name: 'artist',
        props: ['artist']
    }
</script>

<style scoped>
    li {
        display: block;
        margin: 10px 0;
    }
</style>
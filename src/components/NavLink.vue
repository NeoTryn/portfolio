<script setup lang="ts">
    const props = defineProps({
        url : String
    })
</script>

<template>
    <a :href="props.url" id="navLink" target="_blank"><slot>Fallback Content!</slot></a>
</template>

<style>
    @import url('./NavLink.scss');
</style>
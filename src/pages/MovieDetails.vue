<template>
 <DetailsMovie :movieId="movieId" />
</template>

<script setup lang="ts">
import { useRoute } from 'vue-router'
import DetailsMovie from "@/components/movies/DetailsMovie.vue"

const route = useRoute()
const movieId = route.params.id as string
</script>

<style lang="scss" scoped>
h1 {
    color: $white;
    text-align: center;
    margin-top: 50px;
}
</style>
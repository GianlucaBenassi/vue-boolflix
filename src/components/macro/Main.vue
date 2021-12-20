<template>
    <main>
        <MovieCard v-for="(movie, index) in dataShared.movies" :key="index" :infos="movie" type="movie"/>
        <MovieCard v-for="(tvShow, index) in dataShared.tvShows" :key="index" :infos="tvShow" type="tv"/>
    </main>
</template>

<script>
import dataShared from '../../shared/dataShared.js';
import MovieCard from '../parts/MovieCard.vue';

export default {
    name: 'Main',
    components: {
        MovieCard
    },
    data() {
        return {
            dataShared
        }
    }
}
</script>

<style lang="scss" scoped>

</style>
<template>
    <main>
        <MovieCard v-for="(result, index) in dataShared.searchResults" :key="index" :infos="result"/>
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
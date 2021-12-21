<template>
    <main>

        <div v-if="dataShared.movies.length == 0 && dataShared.tvShows.length == 0" class="container">
            <h2>{{dataShared.mainMessage}}</h2>
        </div>

        <div v-else>
            <MovieList/>
            <TvShowList/>
        </div>

    </main>
</template>

<script>
import dataShared from '../../shared/dataShared.js';
import MovieList from '../sections/MovieList.vue';
import TvShowList from '../sections/TvShowList.vue';

export default {
    name: 'Main',
    components: {
        MovieList,
        TvShowList
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
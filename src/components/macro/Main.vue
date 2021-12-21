<template>
    <main>
        <MovieList/>
        <TvShowList/>
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
<template>
    <div class="container">

        <hr class="opacity-100">

        <!-- title -->
        <div class="row">
            <h2 v-if="dataShared.tvShows.length == 0" class="text-center text-md-start mt-2">Nessuna serie tv trovata</h2>
            <h2 v-else class="text-center text-md-start mt-2">Lista serie tv</h2>
        </div>

        <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-4">
            <div class="col" v-for="(tvShow, index) in dataShared.tvShows" :key="index + 20">
                <Card :infos="tvShow" :globalGenres="dataShared.genreList"/>
            </div>
        </div>

    </div>
</template>

<script>
import dataShared from '../../shared/dataShared.js';
import Card from '../parts/Card.vue';

export default {
    name: 'TvShowList',
    components: {
        Card
    },
    data() {
        return{
            dataShared
        }
    }
}
</script>

<style lang="scss" scoped>

hr {
    color: #dc1a28;
    height: 4px;
}

</style>
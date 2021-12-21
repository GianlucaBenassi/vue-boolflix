<template>
    <div class="container">

        <hr class="opacity-100">

        <!-- title -->
        <div class="row">
            <h2 v-if="dataShared.movies.length == 0" class="text-center text-md-start mt-2">Nessun film trovato</h2>
            <h2 v-else class="text-center text-md-start mt-2">Lista film</h2>
        </div>

        <!-- cards -->
        <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-4">
            <div class="col" v-for="(movie, index) in dataShared.movies" :key="index">
                <Card :infos="movie" type="movie"/>
            </div>
        </div>

    </div>
</template>

<script>
import dataShared from '../../shared/dataShared.js';
import Card from '../parts/Card.vue';

export default {
    name: 'MovieList',
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
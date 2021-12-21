<template>
    <div class="container">

        <!-- title -->
        <div class="row">
            <h2 class="text-center text-md-start mt-2">Lista film</h2>
        </div>

        <div class="row">
            <Card v-for="(movie, index) in dataShared.movies" :key="index" :infos="movie" type="movie"/>
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

</style>
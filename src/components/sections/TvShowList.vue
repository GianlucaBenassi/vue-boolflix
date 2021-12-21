<template>
    <div class="container">

        <!-- title -->
        <div class="row">
            <h2 class="text-center text-md-start mt-2">Lista serie tv</h2>
        </div>

        <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-5">
            <div class="col" v-for="(tvShow, index) in dataShared.tvShows" :key="index + 20">
                <Card :infos="tvShow" type="tv"/>
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

</style>
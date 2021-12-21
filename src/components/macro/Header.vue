<template>
    <header>
        <div class="container">
            <div class="row row-cols-1 row-cols-md-2 py-3">

                <div class="col d-flex justify-content-center justify-content-md-start">
                    <img src="../../assets/img/logo.png" alt="Boolflix logo">
                </div>

                <div class="col d-flex justify-content-center justify-content-md-end align-items-center mt-2 mt-md-0">
                    <input type="text" v-model="searchText" @keyup.enter="onSearchMovie()">
                    <button class="ms-1" @click="onSearchMovie()">Search</button>
                </div>

            </div>
        </div>
    </header>
</template>

<script>
import axios from 'axios';
import dataShared from '../../shared/dataShared.js'

export default {
    name: 'Header',
    data() {
        return {
            dataShared,
            searchText: ''
        }
    },
    methods: {
        onSearchMovie: function() {
            if (this.searchText == '') {

                alert('Inserisci un valore corretto!');

            } else {

                // get movies
                axios.get('https://api.themoviedb.org/3/search/movie', {
                    params: {
                    api_key: 'f39e531ef2d1aa05151fd6abd9e8ca67',
                    query: this.searchText,
                    language: 'it-IT'
                    }
                })
                .then(function (response) {
                    dataShared.movies = response.data.results;
                })
                .catch(function (error) {
                    console.log(error);
                }); 

                // get tv show
                axios.get('https://api.themoviedb.org/3/search/tv', {
                    params: {
                    api_key: 'f39e531ef2d1aa05151fd6abd9e8ca67',
                    query: this.searchText,
                    language: 'it-IT'
                    }
                })
                .then(function (response) {
                    dataShared.tvShows = response.data.results;
                })
                .catch(function (error) {
                    console.log(error);
                }); 

            }
        }
    }
}
</script>

<style lang="scss" scoped>

</style>
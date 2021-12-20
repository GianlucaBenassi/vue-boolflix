<template>
    <header>
        <div class="logo">
            ###logo###
        </div>
        <div class="search">
            <input type="text" v-model="searchText" @keyup.enter="onSearchMovie()">
            <button @click="onSearchMovie()">Search</button>
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

                axios.get('https://api.themoviedb.org/3/search/movie', {
                    params: {
                    api_key: 'f39e531ef2d1aa05151fd6abd9e8ca67',
                    query: this.searchText,
                    language: 'it-IT'
                    }
                })
                .then(function (response) {
                    dataShared.searchResults = response.data.results;
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
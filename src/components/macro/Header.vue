<template>
    <header>
        <div class="logo">
            ###logo###
        </div>
        <div class="search">
            <input type="text">
            <button @click="onSearchMovie()">Search</button>
        </div>
    </header>
</template>

<script>
import axios from 'axios';

export default {
    name: 'Header',
    data() {
        return {
            searchText: ''
        }
    },
    methods: {
        onSearchMovie: function() {
            axios.get('https://api.themoviedb.org/3/search/movie', {
                params: {
                api_key: 'f39e531ef2d1aa05151fd6abd9e8ca67',
                query: 'ritorno al futuro'
                }
            })
            .then(function (response) {
                console.log(response.data.results);
            })
            .catch(function (error) {
                console.log(error);
            }); 
        }
    }
}
</script>

<style lang="scss" scoped>

</style>
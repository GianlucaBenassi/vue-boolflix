<template>
    <header>
        <div class="container">
            <div class="row row-cols-1 row-cols-md-2 py-3">

                <div class="col d-flex justify-content-center justify-content-md-start">
                    <img src="../../assets/img/logo.png" alt="Boolflix logo">
                </div>

                <div class="col d-flex justify-content-center justify-content-md-end align-items-center mt-2 mt-md-0">
                    <input type="text" v-model="searchText" @keyup.enter="onSearch()">
                    <button class="ms-1" @click="onSearch()">Search</button>
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
            searchText: '',
            apiKey: 'f39e531ef2d1aa05151fd6abd9e8ca67',
            apiLang: 'it-IT'
        }
    },
    methods: {
        onSearch: function() {
            if (this.searchText == '') {

                alert('Inserisci un valore corretto!');

            } else {
                
                // clear shared data
                this.dataShared.movies = [];
                this.dataShared.tvShows = [];

                // get movies
                axios.get('https://api.themoviedb.org/3/search/movie', {
                    params: {
                        api_key: this.apiKey,
                        query: this.searchText,
                        language: this.apiLang
                    }
                })
                .then((response) => {
                    // add movies to dataShared.movies
                    const movieList = response.data.results;

                    // get movies credits
                    movieList.forEach((elm, index) => {
                        axios.get(`https://api.themoviedb.org/3/movie/${elm.id}/credits`, {
                            params: {
                                api_key: this.apiKey,
                                language: this.apiLang
                            }
                        })
                        .then((response) => {
                            // add cast property to movie object
                            movieList[index].cast = (response.data.cast).slice(0,5);
                            this.dataShared.movies.push(movieList[index]);
                        })
                        .catch(function(error) {
                            console.log(error);
                        });
                    });
                    
                })
                .catch(function (error) {
                    console.log(error);
                }); 


                // get tv show
                axios.get('https://api.themoviedb.org/3/search/tv', {
                    params: {
                        api_key: this.apiKey,
                        query: this.searchText,
                        language: this.apiLang
                    }
                })
                .then((response) => {
                    // add tvShows to dataShared.tvShows
                    const tvShowList = response.data.results;

                    // get tvShow credits
                    tvShowList.forEach((elm, index) => {
                        axios.get(`https://api.themoviedb.org/3/tv/${elm.id}/credits`, {
                            params: {
                                api_key: this.apiKey,
                                language: this.apiLang
                            }
                        })
                        .then((response) => {
                            // add cast property to tvShows object
                            tvShowList[index].cast = (response.data.cast).slice(0,5);
                            this.dataShared.tvShows.push(tvShowList[index]);
                        })
                        .catch(function(error) {
                            console.log(error);
                        });
                    });

                })
                .catch(function (error) {
                    console.log(error);
                });

                // change main message
                dataShared.mainMessage = 'Nessun risultato trovato'

            }
        }
    },
    mounted() {

        // get movies genre list
        const getMoviesGenre = () => {
            return axios.get('https://api.themoviedb.org/3/genre/movie/list', {
                params: {
                    api_key: this.apiKey,
                    language: this.apiLang
                }
            });
        }

        // get tv shows genre list
        const getTvShowsGenre = () => {
            return axios.get('https://api.themoviedb.org/3/genre/tv/list', {
                params: {
                    api_key: this.apiKey,
                    language: this.apiLang
                }
            });
        }

        // axios multi get request for genres
        Promise.all([getMoviesGenre(), getTvShowsGenre()])
        .then((results) => {

            const arrGenreList = results[0].data.genres;
            results[1].data.genres.forEach(elm => {
                arrGenreList.push(elm);
            });

            const notDupId = [];
            arrGenreList.forEach(elm => {
                if (!notDupId.includes(elm.id)) {
                    notDupId.push(elm.id);
                    this.dataShared.genreList.push(elm);
                }
            });

        });

    }
}
</script>

<style lang="scss" scoped>

</style>
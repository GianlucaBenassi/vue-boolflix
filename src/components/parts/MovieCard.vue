<template>
    <div class="card">

        <!-- poster -->
        <img :src="'https://image.tmdb.org/t/p/w342' + infos.poster_path" :alt="'Poster ' + infos.id">

        <!-- title -->
        <h2 v-if="type == 'movie'">{{infos.title}}</h2>
        <h2 v-else>{{infos.name}}</h2>
        <h3 v-if="type == 'movie'">{{infos.original_title}}</h3>
        <h3 v-else>{{infos.original_name}}</h3>

        <!-- language -->
        <span v-if="infos.original_language == ''">Lingua non disponibile</span>
        <img 
            v-else
            :src="require('../../assets/img/flags/' + infos.original_language + '.svg')" 
            :alt="infos.id" 
            class="language">

        <!-- vote -->
        <span class="Vote" v-for="index in stars" :key="index"><i class="fas fa-star"></i></span>

    </div>
</template>

<script>
export default {
    name: 'MovieCard',
    props: {
        infos: Object,
        type: String
    },
    data() {
        return{
            stars: Math.ceil(this.infos.vote_average / 2)
        }
    }
}
</script>

<style lang="scss" scoped>

.card {
    margin: 20px 0;

    .language {
        max-width: 30px;
    }
}

</style>
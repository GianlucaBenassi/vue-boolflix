<template>
    <div class="ms_card">

        <!-- poster -->
        <img class="poster_card" v-if="infos.poster_path == null" src="../../assets/img/no-poster.jpg" :alt="'no poster ' + infos.id">
        <img class="poster_card" v-else :src="'https://image.tmdb.org/t/p/w342' + infos.poster_path" :alt="'Poster ' + infos.id">

        <!-- title -->
        <h3 v-if="type == 'movie'">{{infos.title}}</h3>
        <h3 v-else>{{infos.name}}</h3>
        <h4 v-if="type == 'movie'">{{infos.original_title}}</h4>
        <h4 v-else>{{infos.original_name}}</h4>

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
    name: 'Card',
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

.ms_card {
    margin: 20px 0;

    .poster_card {
        width: 100%;
    }

    .language {
        max-width: 30px;
    }
}

</style>
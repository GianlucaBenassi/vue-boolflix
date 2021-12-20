<template>
    <div class="card">

        <!-- titoli -->
        <h2 v-if="type == 'movie'">{{infos.title}}</h2>
        <h2 v-else>{{infos.name}}</h2>
        <h3 v-if="tyle == 'movie'">{{infos.original_title}}</h3>
        <h3 v-else>{{infos.original_name}}</h3>

        <!-- lingua -->
        <span v-if="infos.original_language == ''">Lingua non disponibile</span>
        <img 
            v-else
            :src="require('../../assets/img/flags/' + infos.original_language + '.svg')" 
            :alt="infos.original_title + ' language ' + infos.original_language" 
            class="language">

        <!-- voto -->
        <span class="Vote">{{infos.vote_average}}</span>

    </div>
</template>

<script>
export default {
    name: 'MovieCard',
    props: {
        infos: Object,
        type: String
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
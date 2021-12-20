<template>
    <div class="card">
        <h2>{{infos.title}}</h2>
        <h3>{{infos.original_title}}</h3>
        <span v-if="infos.original_language == ''">Lingua non disponibile</span>
        <img 
            v-else
            :src="require('../../assets/img/flags/' + infos.original_language + '.svg')" 
            :alt="infos.original_title + ' language ' + infos.original_language" 
            class="language">
        <span class="Vote">{{infos.vote_average}}</span>
    </div>
</template>

<script>
export default {
    name: 'MovieCard',
    props: {
        infos: Object
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
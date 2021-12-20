<template>
    <div class="card">
        <h2>{{infos.title}}</h2>
        <h3>{{infos.original_title}}</h3>
        <span class="language">{{infos.original_language}}</span>
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
}

</style>
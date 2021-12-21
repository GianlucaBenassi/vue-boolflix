<template>
    <div class="ms_card position-relative my-3">

        <!-- poster -->
        <img class="poster_card" v-if="infos.poster_path == null" src="../../assets/img/no-poster.jpg" :alt="'no poster ' + infos.id">
        <img class="poster_card" v-else :src="'https://image.tmdb.org/t/p/w342' + infos.poster_path" :alt="'Poster ' + infos.id">

        <!-- infos -->
        <div class="ms_infos position-absolute top-0 bottom-0 start-0 end-0 p-2">

            <!-- title -->
            <h4 v-if="type == 'movie'">{{infos.title}}</h4>
            <h4 v-else>{{infos.name}}</h4>

            <!-- original title -->
            <span v-if="type == 'movie'" class="d-block mb-2"><strong>Titolo originale:</strong> {{infos.original_title}}</span>
            <span v-else class="d-block mb-2"><strong>Titolo originale:</strong> {{infos.original_name}}</span>

            <!-- vote -->
            <span class="Vote d-block mb-2">
                <strong class="me-2">Voto:</strong>
                <i v-for="index in stars" :key="index" class="fas fa-star"></i>
            </span>

            <!-- language -->
            <img
                v-if="infos.original_language == ''"
                src="../../assets/img/no-flag.png" 
                :alt="'language not available ' + infos.id"
                class="language_icon mb-2">

            <img 
                v-else
                :src="require('../../assets/img/flags/' + infos.original_language + '.svg')" 
                :alt="infos.id" 
                class="language_icon mb-2">

            <!-- overview -->
            <p v-if="infos.overview == ''" class="overflow-hidden"><strong>Overview:</strong> Not available</p>
            <p v-else class="overflow-hidden"><strong>Overview:</strong> {{infos.overview}}</p>

        </div>

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

    .poster_card {
        width: 100%;
        height: 400px;
        object-fit: cover;
        object-position: center;
    }

    .ms_infos {
        color: #fff;
        background-color: rgba(0,0,0,.7);

        .fa-star {
            color: rgb(255, 255, 0);
        }

        .language_icon {
            max-width: 25px;
        }

        p {
            display: -webkit-box;
            -webkit-line-clamp: 4;
            -webkit-box-orient: vertical;  
            overflow: hidden;
        }

    }
}

</style>
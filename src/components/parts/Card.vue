<template>
    <div class="ms_card position-relative my-3">

        <!-- poster -->
        <img
            class="poster_card" 
            :src="infos.poster_path ? 'https://image.tmdb.org/t/p/w342' + infos.poster_path : require('../../assets/img/no-poster.jpg')"
            :alt="'Poster ' + infos.id">

        <!-- infos -->
        <div class="ms_infos position-absolute top-0 bottom-0 start-0 end-0 p-2 d-none">

            <!-- language -->
            <img 
                :src="infos.original_language ? require('../../assets/img/flags/' + infos.original_language + '.svg') : require('../../assets/img/no-flag.png')" 
                :alt="'language for' + infos.id" 
                class="language_icon position-absolute bottom-0 end-0 opacity-75">

            <!-- title -->
            <h4 class="line_clamp_2">{{infos.title || infos.name}}</h4>

            <!-- original title -->
            <span class="mb-2 line_clamp_2"><strong>Titolo originale:</strong> {{infos.original_title || infos.original_name}}</span>

            <!-- vote -->
            <span class="Vote d-block mb-2">
                <strong class="me-2">Voto:</strong>
                <i v-for="index in stars" :key="index" class="fas fa-star"></i>
            </span>

            <!-- overview -->
            <p class="overflow-hidden line_clamp_3"><strong>Overview:</strong> {{infos.overview || 'Not available'}}</p>

            <!-- cast -->
            <p class="line_clamp_3"><strong>Cast:</strong> {{creditsList}}</p>

        </div>

    </div>
</template>

<script>
export default {
    name: 'Card',
    props: {
        infos: Object,
    },
    data() {
        return{
            stars: Math.ceil(this.infos.vote_average / 2)
        }
    },
    computed: {

        creditsList() {
            // get cast list
            if (this.infos.cast.length == 0) {
                return 'Not available'
            } else {
                let list = '';
                this.infos.cast.forEach(elm => {
                    list += elm.name + ', ';
                });
                return list.slice(0, -2);
            }
        }

    }
}
</script>

<style lang="scss" scoped>

.ms_card {
    cursor: pointer;

    &:hover .ms_infos {
        display: block !important;
    }

    .poster_card {
        width: 100%;
        height: 380px;
        object-fit: cover;
        object-position: center;

        @media screen and (max-width: 576px) {
            height: auto;
        }
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

    }
}

</style>
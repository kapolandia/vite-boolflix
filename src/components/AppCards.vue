<script>
    import { store } from '../store.js';

    export default{
        name: "AppCards",
        data(){
            return{
                store: store,
            };
        },
        methods:{
            getSrcFromApi(poster){
                return `https://image.tmdb.org/t/p/w342${poster}`;
            },
            clipText(text, maxChars) {
            if (text.length > maxChars) {
                return text.slice(0, maxChars) + '...';
            } else {
                return text;
            }
        }
        },
        mounted(){
            console.log(store.searchResult);
        }
    }
</script>

<template>
    <div class="row justify-content-center align-items-center mx-0">
        <div class="col-3 my-3" v-for="film in store.searchResult" style="position: relative;">
            <div class="film-container">
                <img :src="getSrcFromApi(film.poster_path)" alt="">
                <div class="my-description">
                    <p class="m-0"><b>Titolo:</b> {{ film.title }}</p>
                    <p class="m-0"><b>Titolo originale:</b> {{ film.original_title }}</p>
                    <p class="m-0"><b>Lingua:</b> 🇮🇹</p>
                    <p class="m-0">
                        <b>Rating: ⭐️</b>
                        <span v-if="film.vote_average > 2">⭐️</span>
                        <span v-if="film.vote_average > 4">⭐️</span>
                        <span v-if="film.vote_average > 6">⭐️</span>
                        <span v-if="film.vote_average > 8">⭐️</span>
                    </p>
                    <p class="m-0"><b>Overview:</b> {{ clipText(film.overview, 150) }}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<style>
    .film-container {
        position: relative;
        cursor: pointer;
        overflow: hidden;
    }

    .film-container img {
        display: block;
        width: 100%;
        height: auto;
    }

    .film-container .my-description {
        position: absolute;
        display: none;
        top: 10px;
        left: 30px; 
        color: white; 
        padding: 5px 10px;
    }

    .film-container:hover img {
        opacity: calc(10%);
        transition: ease 0.2s;
    }

    .film-container:hover .my-description {
        display: block;
    }
</style>


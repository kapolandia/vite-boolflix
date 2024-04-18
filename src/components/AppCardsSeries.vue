<script>
    import { store } from '../store.js';

    export default{
        name: "AppCardsSeries",
        data(){
            return{
                store: store,
                arrowVar: 0,
                movedRight: 0,
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
            },
            moveRight(){
                if(store.searchResultSeries.length > ((this.movedRight * 2) +2) && store.searchResultSeries.length > 4){
                    this.arrowVar -= 660;
                    this.movedRight += 1;
                    console.log(this.movedRight)
                }
            },
            moveLeft(){
                if(this.arrowVar != 0){
                    this.arrowVar += 660;
                    this.movedRight -= 1;
                }
            }
        },

    }
</script>

<template>
    <div style="margin-bottom: 510px;">
        <div>
            <button class="my-arrow" @click="moveLeft"><i class="fa-solid fa-chevron-left" @click="moveLeft"></i></button>
        </div>
        <div>
            <button class="my-arrow-right" @click="moveRight"><i class="fa-solid fa-chevron-right" @click="moveRight"></i></button>
        </div>
        <h2 class="m-3 text-white" >Serie TV</h2>
        <div class="my-row  align-items-center mx-0" :style="{left: this.arrowVar + 'px'}">
            <div class="m-3" v-for="film, index in store.searchResultSeries" >            
                <div class="film-container rounded">
                    <img v-if="film.poster_path" :src="getSrcFromApi(film.poster_path)" alt="">
                    <img v-else src="https://w0.peakpx.com/wallpaper/172/343/HD-wallpaper-netflix-logo-black-logo-minimal-netflix.jpg" alt="" style="max-width: 342px;aspect-ratio: 1.3/2;">
                    <div class="my-description">
                        <p class="m-0"><b>Titolo:</b> {{ film.name }}</p>
                        <p class="m-0"><b>Titolo originale:</b> {{ film.original_name }}</p>
                        <p class="m-0">
                            <b>Lingua:</b>
                            <span v-if="film.original_language == 'it'">🇮🇹</span>
                            <span v-else-if="film.original_language == 'en'">🏴󠁧󠁢</span>
                            <span v-else>🏴</span>
                        </p>
                        <p class="m-0">
                            <b>Rating: ⭐️</b>
                            <span v-if="film.vote_average > 2">⭐️</span>
                            <span v-if="film.vote_average > 4">⭐️</span>
                            <span v-if="film.vote_average > 6">⭐️</span>
                            <span v-if="film.vote_average > 8">⭐️</span>
                        </p>
                        <p class="m-0"><b>Overview:</b> {{ clipText(film.overview, 330) }}</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .film-container {
        position: relative;
        cursor: pointer;
        overflow: hidden;
    }

    .my-row{
        flex-wrap: nowrap;
        display: flex;
        overflow-x: hidden;
        position: absolute;
        transition: left 0.3s ease;
    }

    .film-container img {
        display: block;
        width: 300px;
        height: 450px;
        background-size: cover;
        transition: transform 0.3s ease;
    }

    .film-container .my-description {
        position: absolute;
        display: none;
        top: 10px; 
        color: white; 
        padding: 20px;
        width: 300px;
    }

    .film-container:hover img {
        opacity: calc(10%);
        transition: ease 0.2s;
        transform: scale(1.2);
    }

    .film-container:hover .my-description {
        display: block;
    }

    .my-arrow{
        position: absolute;
        left: 0;
        top: 910px;
        z-index: 2;
        background-color: rgba(37, 37, 37, 0.732);
        border: none;
        padding: 10px;
        border-top-right-radius: 10px;
        border-bottom-right-radius: 10px;
        color: rgb(255, 255, 255);
        font-size: 40px;
        cursor: pointer;
    }

    .my-arrow-right{
        position: absolute;
        right: 0;
        top: 910px;
        z-index: 2;
        background-color: rgba(37, 37, 37, 0.732);
        border: none;
        padding: 10px;
        border-top-left-radius: 10px;
        border-bottom-left-radius: 10px;
        color: rgb(255, 255, 255);
        font-size: 40px;
        cursor: pointer;
    }
</style>


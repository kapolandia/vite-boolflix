<script>
import axios from 'axios';
import { store } from '../store.js';

    export default{
        name: "AppHeader",
        data(){
            return{
                store,
                searchCall: "",
            };
        },
        methods: {
            searchCallApi() {
                axios.get('https://api.themoviedb.org/3/search/movie?',{
                    params: {
                        api_key: "9d769840d258dadf154fb965f491f4bb",
                        query: this.searchCall,
                        language: "it-IT"
                    }
                })
                    .then((response) => {
                    store.searchResult = [];
                    store.searchResult = response.data.results;
                    console.log(store.searchResult);
                });
            },
        }
    }
</script>

<template>
<nav class="navbar navbar-expand-lg" style="background-color: #1C1C1C;">
  <div class="container-fluid">
    <a class="navbar-brand text-white" href="#">BOOLFLIX</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">

      <form class="d-flex ms-auto" role="search">
        <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search" v-model="searchCall">
        <button class="btn btn-danger" @click="this.searchCallApi" >Search</button>
      </form>
    </div>
  </div>
</nav>
</template>

<style scoped>
</style>
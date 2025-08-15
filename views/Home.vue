<script setup>
import {ref} from 'vue'
import env from '@/env.js'

const search = ref('');
const movies = ref ([]);

const SearchMovies = () => {
  if(search.value != '') {
    fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
      .then(response => response.json())
      .then(data => {
        movies.value = data.Search || [];
        search.value = '';
      })
  }
}
</script>

<template>
  <div class='home'>
    <header>
      <h1>Introducing MovieFinder</h1>
      <p class='header_description'>Discover your next favorite film with our smart, fast, most useful movie search yet, with recommendations built in — so you get the best movies, every time.</p>
    </header>
    <form @submit.prevent='SearchMovies()' class='search_box'>
      <input type='text' placeholder='Начни Поиск' v-model='search'/>
    </form>
    <div class='movies_list'>
      <div class='movies' v-for='movie in movies' :key='movie.imdbID'>
        <router-link :to="'/movie/' + movie.imdbID" class='movies_link'>
          <div class='movies_image'>
            <img :src='movie.Poster' alt='Poster'>
            <div class='type'>{{ movie.Type }}</div>
          </div>
          <div class='detail'>
            <p class='movies_year'>{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>


<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

header {
  text-align: center;
  margin-bottom: 4rem;
}

a {
  text-decoration: none;
}

h1 {
  font-size: 4rem;
  font-weight: 600;
  line-height: 1;
  color: rgb(30, 41, 57);
  animation: float-animation 6s ease-in-out infinite;
}

@keyframes float-animation {
0%, 100% {
  transform: translateY(0px);
}
50% {
  transform: translateY(-10px);
}
}

.home header .header_description {
  color: rgb(74, 85, 101);
  font-size: 1.25rem;
  max-width: 42rem;
  margin-inline: auto;
  line-height: 1.625;
}

.home .search_box {
  background: #ffffffe6;
  border: 1px solid #0000001a;
  transition: all .2s;
}

.home .movies_list {
  display: flex;
  flex-wrap: wrap;
  margin: 0rem 0.5rem;
}


.home .movies_list .movies {
  max-width: 50%;
  flex: 1 1 50%;
  padding: 0.8rem 1rem;
}


.home .movies_list .movies .movies_link {
  display: flex;
  flex-direction: column;
  height: 100%;
}

.home .movies_list .movies .movies_link:hover {
  border: 4px solid var(--yellow);
  transition: 0.5s;
}

.home .movies_list .movies .movies_link .movies_image{
  position: relative;
  display: block;
}


.home .movies_list .movies .movies_link .movies_image img{
  display: block;
  width: 100%;
  height: 17rem;
  object-fit: cover;

}

.home .movies_list .movies .movies_link .movies_image .type{
  position: absolute;
  padding: 0.5rem 1rem;
  background-color: var(--orange);
  color: var(--yellow);
  bottom: 1rem;
  left: 0rem;
  text-transform: capitalize;
}


.home .movies_list .movies .movies_link .detail {
  background-color: var(--orange);
  padding: 1rem 0.5rem;
  flex: 1 1 100%;
  border-radius: 0rem 0rem 0.5rem 0.5rem;
}



.home .movies_list .movies .movies_link .detail .movies_year {
  color: #ccb000;
  font-size: 0.8rem;
  padding-bottom: 0.4.rem;
}

.home .movies_list .movies .movies_link .detail {
  color: var(--yellow);
  font-weight: 600;
  font-size: 1.1rem
}
</style>

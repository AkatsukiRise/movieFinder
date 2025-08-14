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
    <div class='feature_card'>
      <router-link to='/movie/tt3783958'>
        <img src='https://mir-s3-cdn-cf.behance.net/project_modules/disp/6ae75746996947.586cfecbef3b1.jpg' alt='La-La-Land' class='feature_img'>
        <div class='detail'>
          <h3>La La Land</h3>
          <p>Mia, an aspiring actress, serves lattes to movie stars in between auditions and Sebastian, a jazz musician, scrapes by playing cocktail party gigs in dingy bars, but as success mounts they are faced with decisions that begin to fray the fragile fabric of their love affair, and the dreams they worked so hard to maintain in each other threaten to rip them apart</p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent='SearchMovies()' class='search_box'>
      <input type='text' placeholder='Начни Поиск' v-model='search'/>
      <input type='submit' value='Поиск'>
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

.home .feature_card {
  position: relative;
}

.home .feature_card .feature_img {
  display: block;
  margin: auto;
  width: 12.5rem;
  height: 25rem;
  object-fit: cover;
  position: relative;
  z-index: 0;
}

.home .feature_card .detail {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.6);
  padding: 1rem;
  z-index: 1;
}

.home .feature_card .detail h3 {
  color: #fff;
  margin: 1rem;
  text-decoration: none;
}

.home .feature_card .detail p {
  color: #fff;
  text-decoration: none;
}

.home .search_box {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 1rem;
}

.home .search_box input[type='text'] {
  width: 100%;
  color: #fff;
  background-color: #496583;
  font-size: 1.35rem;
  padding: 0.7rem 1rem;
  border-radius: 0.5rem;
  margin-bottom: 0.9rem;
  transition: 0.4s;
}

.home .search_box input[type='text']::placeholder {
  color: #f3f3f3;
}

.home .search_box input[type='text']:focus {
  box-shadow: 0px 0.25rem 0.5rem rgba(0, 0, 0, 0.2);
}

.home .search_box input[type='submit'] {
  width: 100%;
  max-width: 300px;
  background-color: var(--orange);
  padding: 1rem;
  border-radius: 0.5rem;
  color: var(--yellow);
  font-size: 1.25rem;
  text-transform: uppercase;
  transition: 0.4s;
}

.home .search_box input[type='submit']:active {
  background-color: var(--red);
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

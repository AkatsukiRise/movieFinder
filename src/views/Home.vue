<script setup>
import {ref} from 'vue'
import env from '@/env.js'

const search = ref('');
const movies = ref([]);
const page = ref(1);

const searchMovies = () => {
  if(search.value.trim() != '') {
    fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}&page=${page.value}`)
      .then(response => response.json())
      .then(data => {
        movies.value = data.Search || [];
      })
  }
}

function scrollToTop() {
          window.scrollTo({
            top: 0,
            left: 0,
          });
        }
</script>

<template>
  <header>
    <router-link to='/'>
      <h1>Introducing MovieFinder</h1>
    </router-link>
    <p class='header-description'>Discover your next favorite film with our smart, fast, most useful movie search yet, with recommendations built in — so you get the best movies, every time.</p>
  </header>

  <div class='search-box'>
    <form @submit.prevent='searchMovies' class='search-form'>
      <input type='text' class='search-input' placeholder='Start your journey' v-model='search'/>
    </form>
  </div>
  <div v-if='!movies.length' class='welcome-container'>
    <img src='../../favicon.jpeg' width='64' height='64' class='welcome-icon' alt='icon'>
    <h2>Ready to discover movies?</h2>
    <p>Start by searching for a movie above and find your next favorite film</p>
  </div>

  <div v-else>
    <div class='movies-list'>
      <div class='movies' v-for='movie in movies' :key='movie.imdbID'>
        <router-link :to="'/movie/' + movie.imdbID" class='movies-link'>
          <div class='movies-image'>
            <img :src='movie.Poster' alt='movie.Title + Poster'>
            <div class='type'>{{ movie.Type }}</div>
          </div>
          <div class='detail'>
            <p class='movies-year'>{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
    <div class='page-first'>
      <button v-if='page > 1' @click='page = 1; searchMovies()' class='page' id='first'>
        Вернуться на первую страницу
      </button>
      <div class='page-container'>
        <button v-if='page > 1' @click='page--; scrollToTop(); searchMovies()' class='page'>
          Предыдущая
        </button>
        <p>Страница {{page}}</p>
        <button @click='page++; scrollToTop(); searchMovies()' class='page'>
          Следующая
        </button>
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
  color: var(--black);
  animation: float-animation 6s ease-in-out infinite;
}

h2 {
  color: var(--black);
  font-size: 1.5rem;
  line-height: 2rem;
  font-weight: 600;
}

@keyframes float-animation {
0%, 100% {
  transform: translateY(0px);
}
50% {
  transform: translateY(-10px);
}
}

header .header-description {
  color: rgb(74, 85, 101);
  font-size: 1.25rem;
  max-width: 42rem;
  margin-inline: auto;
  line-height: 1.625;
}

.search-box {
  max-width: 48rem;
  margin-inline: auto;
  margin-bottom: 3rem;
  position: relative;
}

.search-box .search-form {
  display: flex;
  align-items: center;
}

.search-box .search-input {
  display: flex;
  height: 4rem;
  width: 100%;
  background: #ffffffe6;
  border: 1px solid #0000001a;
  border-radius: 9999px;
  padding-inline: .75rem;
  padding-block: .25rem;
  box-shadow: 0 0 #0000, 0 0 #0000, 0 0 #0000, 0 1px 2px 0 rgba(0, 0, 0, 0.05);
  outline-style: none;
  font-size: 1.1rem;
}

.welcome-container {
  padding-top: 4rem;
  padding-bottom: 4rem;
  margin: auto;
  max-width: 32rem;
  text-align: center;

}

.welcome-container .welcome-icon {
  border-radius: 50%;
}

.welcome-container p {
  color: #4b5563;
  font-size: 1.125rem;
  line-height: 1.75rem;
}

.movies-list {
  display: flex;
  flex-wrap: wrap;
  margin: 0rem 0.5rem;
}


.movies-list .movies {
  max-width: 20%;
  flex: 1 1 20%;
  padding: 0.8rem 1rem;
}


.movies-list .movies .movies-link {
  display: flex;
  flex-direction: column;
  height: 100%;
  background: rgba(255, 255, 255, 0.8);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(0, 0, 0, 0.1);
  border-radius: 0.5rem 0.5rem 0.5rem 0.5rem;
  transition: all 0.3s ease;
}

.movies-list .movies .movies-link:hover {
  background: rgba(255, 255, 255, 0.95);
  transform: translateY(-4px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

.movies-list .movies .movies-link .movies-image{
  position: relative;
  display: block;
}

.movies-list .movies .movies-link .movies-image img{
  display: block;
  width: 100%;
  height: 17rem;
  object-fit: cover;
  border-radius: 0.5rem 0.5rem 0 0;
}

.movies-list .movies .movies-link .movies-image .type{
  position: absolute;
  padding: 0.5rem 1rem;
  background-color: var(--white);
  color: var(--black);
  bottom: 1rem;
  left: 0rem;
  text-transform: capitalize;
}


.movies-list .movies .movies-link .detail {
  background-color: var(--white);
  padding: 1rem 0.5rem;
  flex: 1 1 100%;
  border-radius: 0rem 0rem 0.5rem 0.5rem;
}

.movies-list .movies .movies-link .detail .movies-year {
  color: #6b7280;
  font-size: 0.8rem;
  font-weight: 500;
  padding-bottom: 0.4rem;
}

.movies-list .movies .movies-link .detail {
  color: var(--black);
  font-weight: 600;
  font-size: 1.1rem
}

.page-first {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.page-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.page-container p {
  width: 6rem;
}

.page {
  width: 8rem;
  height: 2.5rem;
  font-size: 1rem;
  margin-inline: 2.8rem;
  background: #ffffffe6;
  color: var(--black);
  border-radius: .5rem;
  border: 1px solid #0000001a;
}

#first {
  width: 33%;
  margin-bottom: 1rem;
}

@media screen and (max-width: 450px) {
  header {
    margin-bottom: 2rem;
  }

  h1 {
    font-size: 3rem;
  }

  header .header-description {
    max-width: 20rem;
  }

  .search-box {
    max-width: 20rem;
  }

  .movies-list .movies {
    max-width: 50%;
    flex: 1 1 50%;
  }
}


@media screen and (min-width: 451px) and (max-width: 950px) {
  .movies-list .movies {
    max-width: 33%;
    flex: 1 1 33%;
  }

  .movies-list .movies .movies-link .movies-image img {
    height: 100%;
  }
}

@media screen and (min-width: 951px) and (max-width: 1200px) {
  .movies-list .movies {
    max-width: 25%;
    flex: 1 1 25%;
  }

  .movies-list .movies .movies-link .movies-image img {
    height: 100%;
  }
}
</style>

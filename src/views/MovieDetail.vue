<script setup>
import {ref, onBeforeMount} from 'vue';
import {useRoute} from 'vue-router';

const movie = ref({});
const route = useRoute();

onBeforeMount(() => {
  fetch(`http://www.omdbapi.com/?apikey=${import.meta.env.VITE_API_KEY}&i=${route.params.id}&plot=full`)
    .then(response => response.json())
    .then(data => {
      movie.value = data;
    })
});
</script>

<template>
  <div class='movie-detail'>
    <h2>{{movie.Title}}</h2>
    <p>{{ movie.Year }}</p>
    <img :src='movie.Poster' alt='Poster' class='featured-img'>
    <p>{{ movie.Plot }}</p>
  </div>
</template>

<style>
.movie-detail {
  padding: 1rem;
}

.movie-detail h2 {
  color: var(--black);
  font-size: 1.75rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.movie-detail .featured-img {
  display: block;
  max-width: 12.5rem;
  margin-bottom: 1rem;
}

.movie-detail p {
  color: var(--black);
  font-size: 1.2rem;
  line-height: 1.4;
}
</style>

<template>
  <router-link :to="'/movie/' + movie.imdbID" class="movies-link">
    <div class="movies-image">
      <img :src="movie.Poster" :alt="movie.Title + ' Poster'" />
      <div class="type">{{ movie.Type }}</div>
    </div>
    <div class="detail">
      <p class="movies-year">{{ movie.Year }}</p>
      <h3>{{ movie.Title }}</h3>
    </div>
  </router-link>
</template>

<script setup>
const props = defineProps({
  movie: {
    type: Object,
    required: true,
  },
})
</script>

<style scoped>

.movies-link {
  display: flex;
  flex-direction: column;
  height: 100%;
  background: rgba(255, 255, 255, 0.8);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(0, 0, 0, 0.1);
  border-radius: 0.5rem 0.5rem 0.5rem 0.5rem;
  transition: all 0.3s ease;
}

.movies-link:hover {
  background: rgba(255, 255, 255, 0.95);
  transform: translateY(-4px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}


.movies-link .movies-image{
  position: relative;
  display: block;
}

.movies-link .movies-image img{
  display: block;
  width: 100%;
  height: 17rem;
  object-fit: cover;
  border-radius: 0.5rem 0.5rem 0 0;
}

.movies-link .movies-image .type{
  position: absolute;
  padding: 0.5rem 1rem;
  background-color: var(--white);
  color: var(--black);
  bottom: 1rem;
  left: 0rem;
  text-transform: capitalize;
}


.movies-link .detail {
  background-color: var(--white);
  padding: 1rem 0.5rem;
  flex: 1 1 100%;
  border-radius: 0rem 0rem 0.5rem 0.5rem;
}

.movies-link .detail .movies-year {
  color: #6b7280;
  font-size: 0.8rem;
  font-weight: 500;
  padding-bottom: 0.4rem;
}

.movies-link .detail {
  color: var(--black);
  font-weight: 600;
  font-size: 1.1rem
}
</style>

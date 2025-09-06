<template>
  <div class='movie-card'>
    <div class='movie-image'>
    </div>
    <div class='detail'>
      <div class='movie-placeholder'></div>
      <div class='movie-placeholder'></div>
    </div>
  </div>
</template>

<script setup>
</script>

<style scoped>
.movie-card {
  display: flex;
  flex-direction: column;
  height: 375px;
  width: 13rem;
  background: rgba(255, 255, 255, 0.8);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(0, 0, 0, 0.1);
  border-radius: 0.5rem 0.5rem 0.5rem 0.5rem;
}

.movie-image {
  height: 17rem;
  width: 100%;
  background: var(--black);
}

.movie-placeholder {
  margin-left: .5rem;
  width: 1rem;
  height: .3rem;
  background-color: var(--black);
}
</style>

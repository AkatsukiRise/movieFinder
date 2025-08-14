<script setup></script>

<template>
  <div id='container'>
    <header>
      <router-link to='/'>
        <h2><span>Bob</span>Cinema</h2>
        </router-link>
    </header>
    <main>
      <router-link />
    <div id='search_flex'>
    <label for='search'>Искать Фильм</label>
      <input
        id='search'
        placeholder='Название Фильма'
      >
    </div>
    </main>
  </div>
</template>

<style scoped>
:global(:root) {
  --yellow: #FFDC00;
  --red: #1e0700;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;
}

#container {
  max-width: 50rem;
  margin: auto;
}

h2 {
  font-size: 2.2rem;
  color: var(--yellow)
}

router-link {
  all: unset;
}

label {
  margin-right: 2rem;
}

#search {
  width: 15rem;
  height: 2rem;
  border-radius: 1.5rem;
}

#search_flex {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>

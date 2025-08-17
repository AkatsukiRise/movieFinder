<script setup></script>

<template>
  <div id='container'>
    <header>
      <router-link to='/'>
        </router-link>
    </header>
    <main>
      <router-view />
    </main>
  </div>
</template>

<style scoped>
:global(:root) {
  --yellow: #FFDC00;
  --red: #830000;
  --orange: #6b2b00;
  --darkblue: #01000A;
  --black: rgb(30, 41, 57);
  --white: #fffffff2;
}

:global(body){
  background: linear-gradient(135deg, #fdf2f8 0%, #fce7f3 25%, #e0e7ff 50%, #dbeafe 75%, #f0f9ff 100%)
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;
}

#container {
  max-width: 72rem;
  width: 100%;
  margin: auto;
  padding-block: 4rem;
  padding-inline: 1rem;
  margin-inline: auto;
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

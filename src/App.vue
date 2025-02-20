<script setup>
import { RouterLink, RouterView } from "vue-router";

import { onMounted } from "vue";
</script>

<template>
  <header>
    <RouterLink to="/">
      <img alt="SD Pizzas" class="logo" src="@/assets/logo.png" />
    </RouterLink>

    <div class="wrapper">
      <nav>
        <RouterLink to="/menu">MENU</RouterLink>
        <RouterLink to="/about">SOBRE NÓS</RouterLink>
        <RouterLink to="/login">LOGIN</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
  background-color: #3e2d1e;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  display: flex;
}

nav a {
  padding: 0 1rem;
  background: #ebd4a4;
  margin: 24px;
  font-size: 24px;
  border-radius: 99px;
  text-decoration: none;
  color: #d1853a;
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>

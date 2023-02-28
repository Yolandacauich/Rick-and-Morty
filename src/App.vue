<script setup>
import { RouterLink, RouterView } from "vue-router";
import HelloWorld from "./components/HelloWorld.vue";
</script>

<template>

  <nav class=" mx-auto font-medium place-items-start">
        <RouterLink to="/">INICIO</RouterLink>
        <RouterLink to="/personajes">PERSONAJES</RouterLink>
        <RouterLink to="/about">ACERCA DE</RouterLink>
  </nav>
  <header>
    <img class="place-items-center"
      alt="Vue logo"
      src="@/assets/OIP-removebg-preview.png"
      width="195"
      height="185"
    />

    <div class="wrapper">
      <HelloWorld msg="PERSONAJES DE RICK & MORTY" />
    </div>

  </header>

  <RouterView />
</template>

<style scoped>

header {
  line-height: 1.5;
  max-height: 100vh;
  text-align: center;
  margin-left: 10rem;
}
.logo {
  display: block;
  margin: 0 auto 2rem;
}
nav {
  width: 100%;
  font-size: 1.3rem;
  text-align: center;
  margin-top: 2rem;

}
nav a.router-link-exact-active {
  color: var(--color-text);
}
nav a.router-link-exact-active:hover {
  background-color: transparent;
}
nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}
nav a:first-of-type {
  border: 0;
}
@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }
  .logo {
    margin: 0 2rem 0 0;
  }
  header .wrapper {
    display: flex;
    place-items: center;
    flex-wrap: wrap;
  }
  nav {
    text-align: left;
    font-size: 1.3rem;
    padding: 1rem 0;
    margin-top: 1rem;


  }
}
</style>
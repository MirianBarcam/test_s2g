<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />
    <nav class="link-nav">
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/about">About</RouterLink>
    </nav>
  </header>

  <RouterView />
</template>

<style scoped>
.link-nav {
  align-items: center;
  justify-content: end;
  display: flex;
  flex-direction: row;
  gap: 1rem;
  padding: 2rem;
}
header {
  flex-shrink: 0;
  display: flex;
  flex-direction: row;
}

.logo {
  display: block;
}

nav {
  width: 100vw;
  font-size: 12px;
  text-align: center;
  margin: 1.5rem;
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
</style>

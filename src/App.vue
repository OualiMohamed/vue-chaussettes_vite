<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
// import './assets/style.css'
</script>

<template>
  <header>
    <div class="nav-bar">
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <main>
    <RouterView />
  </main>
</template>

<style scoped>
/* 1. Center the links vertically inside the 60px nav-bar */
.nav-bar {
  display: flex;
  align-items: center;
  padding: 0 30px;
}

/* 2. Remove the old margin-top and space the links out */
nav {
  display: flex;
  gap: 15px;
}

/* 3. Style the links with white text and smooth hover */
nav a {
  display: inline-block;
  color: #ffffff;
  text-decoration: none;
  font-size: 18px;
  font-weight: 600;
  padding: 6px 14px;
  border-radius: 6px;
  border: none;
  transition: all 0.2s ease-in-out;
}

/* 4. Hover effect (subtle translucent highlight) */
nav a:hover {
  background-color: rgba(255, 255, 255, 0.25);
  color: #ffffff;
}

/* 5. Active route indicator (using the theme's dark button color #39495c) */
nav a.router-link-exact-active {
  background-color: #39495c;
  color: #ffffff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}
</style>

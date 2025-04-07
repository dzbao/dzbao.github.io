<!--
 * @Date: 2025-04-06 17:05:49
 * @LastEditTime: 2025-04-06 17:42:53
 * @FilePath: \个人博客\my-blog\src\App.vue
-->
<script setup>
import { RouterView } from 'vue-router'
</script>

<template>
  <div class="app-container">
    <nav class="navbar">
      <div class="nav-content">
        <router-link to="/" class="nav-brand">Dezheng Bao</router-link>
        <div class="nav-links">
          <router-link to="/" class="nav-link">Home</router-link>
          <router-link to="/projects" class="nav-link">Projects</router-link>
          <router-link to="/publications" class="nav-link">Publications</router-link>
        </div>
      </div>
    </nav>
    
    <main class="main-content">
      <RouterView />
    </main>
  </div>
</template>

<style>
.app-container {
  min-height: 100vh;
  background-color: #0a192f;
}

.navbar {
  background-color: rgba(10, 25, 47, 0.9);
  backdrop-filter: blur(10px);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  padding: 1rem 0;
}

.nav-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-brand {
  color: #64ffda;
  font-size: 1.5rem;
  font-weight: bold;
  text-decoration: none;
  transition: color 0.3s ease;
}

.nav-brand:hover {
  color: #88a2ff;
}

.nav-links {
  display: flex;
  gap: 2rem;
}

.nav-link {
  color: #ccd6f6;
  text-decoration: none;
  font-size: 1rem;
  transition: all 0.3s ease;
  position: relative;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0;
  height: 2px;
  background: #64ffda;
  transition: width 0.3s ease;
}

.nav-link:hover {
  color: #64ffda;
}

.nav-link:hover::after {
  width: 100%;
}

.router-link-active {
  color: #64ffda;
}

.router-link-active::after {
  width: 100%;
}

@media (max-width: 768px) {
  .nav-content {
    padding: 0 1rem;
  }
  
  .nav-links {
    gap: 1rem;
  }
}

.main-content {
  flex: 1;
  /* padding: 2rem; */
}
</style>


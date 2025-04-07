<script setup>
import { ref, onMounted } from 'vue'
import project1 from '@/assets/images/project1.jpg'
import project2 from '@/assets/images/project2.jpg'
import project3 from '@/assets/images/project3.jpg'
const projects = ref([
  {
    title: 'Review System for State Grid Projects',
    description: 'An LLM-based review system for multi-disciplinary and multi-category projects of the State Grid.',
    image: project3,
    link: ''
  },
  {
    title: 'Avator Making Mini Program on WeChat',
    description: 'A WeChat mini program for Spring Festival avator making.',
    image: project2,
    link: 'https://github.com/dzbao/ZJUSpringFestivalAvatar'
  },
  {
    title: 'MicroPython VSCode Plugins for ESP32',
    description: 'A tool for writing MicroPython on esp32, as the course assignment of ZJU Embedded System by Kai Weng.',
    image: project1,
    link: 'https://github.com/zpqqq10/grand-Unified-Theory'
  }
])

onMounted(() => {
  // 可以在这里添加加载动画
})
</script>

<template>
  <div class="projects-container">
    <h1>Projects</h1>
    <div class="projects-list">
      <div v-for="(project, index) in projects" :key="index" class="project-card">
        <div class="project-image">
          <img :src="project.image" :alt="project.title">
        </div>
        <div class="project-content">
          <h2>{{ project.title }}</h2>
          <p>{{ project.description }}</p>
          <a :href="project.link" target="_blank" class="project-link">View Project</a>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.projects-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 6rem 2rem 2rem;
  min-height: 100vh;
  background-color: #0a192f;
  color: #e6f1ff;
}

h1 {
  color: #64ffda;
  margin-bottom: 3rem;
  font-size: 2.5rem;
  position: relative;
}

h1::after {
  content: '';
  position: absolute;
  bottom: -0.5rem;
  left: 0;
  width: 60px;
  height: 4px;
  background: linear-gradient(90deg, #64ffda, transparent);
}

.projects-list {
  display: grid;
  gap: 3rem;
}

.project-card {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 2rem;
  background: rgba(255, 255, 255, 0.05);
  padding: 2rem;
  border-radius: 8px;
  backdrop-filter: blur(10px);
  transition: transform 0.3s ease;
}

.project-card:hover {
  transform: translateY(-5px);
}

.project-image {
  position: relative;
  overflow: hidden;
  border-radius: 8px;
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}


.project-card:hover .project-image img {
  transform: scale(1.05);
}

.project-content {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.project-content h2 {
  color: #64ffda;
  margin-bottom: 1rem;
  font-size: 1.5rem;
}

.project-content p {
  color: #8892b0;
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.project-link {
  display: inline-block;
  padding: 0.5rem 1rem;
  background: transparent;
  border: 2px solid #64ffda;
  color: #64ffda;
  text-decoration: none;
  border-radius: 4px;
  transition: all 0.3s ease;
  align-self: flex-start;
}

.project-link:hover {
  background: rgba(100, 255, 218, 0.1);
  transform: translateY(-2px);
}

@media (max-width: 768px) {
  .project-card {
    grid-template-columns: 1fr;
  }
  
  .project-image {
    height: 200px;
  }
}
</style> 
<script setup>
const projects = [
  {
    title: 'Project 3',
    description: 'Description of project 1',
    image: '@/assets/project3.jpg',
    githubLink: 'https://github.com/yourusername/project1'
  },
  {
    title: 'Project 1',
    description: 'Description of project 1',
    image: '@/assets/project1.jpg',
    githubLink: 'https://github.com/yourusername/project1'
  },
  {
    title: 'Project 2',
    description: 'Description of project 2',
    image: '@/assets/project2.jpg',
    githubLink: 'https://github.com/yourusername/project2'
  }
]
</script>

<template>
  <div class="activities-container">
    <h1>Activities</h1>
    <div class="activities-list">
      <div v-for="(activity, index) in activities" :key="index" class="activity-card">
        <div class="activity-image">
          <img :src="activity.image" :alt="activity.title">
        </div>
        <div class="activity-content">
          <h2>{{ activity.title }}</h2>
          <p>{{ activity.description }}</p>
          <a :href="activity.link" target="_blank" class="activity-link">View Project</a>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.activities-container {
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

.activities-list {
  display: grid;
  gap: 3rem;
}

.activity-card {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 2rem;
  background: rgba(255, 255, 255, 0.05);
  padding: 2rem;
  border-radius: 8px;
  backdrop-filter: blur(10px);
  transition: transform 0.3s ease;
}

.activity-card:hover {
  transform: translateY(-5px);
}

.activity-image {
  position: relative;
  overflow: hidden;
  border-radius: 8px;
}

.activity-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.activity-card:hover .activity-image img {
  transform: scale(1.05);
}

.activity-content {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.activity-content h2 {
  color: #64ffda;
  margin-bottom: 1rem;
  font-size: 1.5rem;
}

.activity-content p {
  color: #8892b0;
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.activity-link {
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

.activity-link:hover {
  background: rgba(100, 255, 218, 0.1);
  transform: translateY(-2px);
}

@media (max-width: 768px) {
  .activity-card {
    grid-template-columns: 1fr;
  }
  
  .activity-image {
    height: 200px;
  }
}
</style> 
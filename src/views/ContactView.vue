<script setup>
const contactInfo = {
  email: 'your.email@example.com',
  wechat: 'your_wechat_id',
  location: 'Zhejiang University, Hangzhou, China'
}

const socialLinks = [
  {
    platform: 'GitHub',
    icon: 'fab fa-github',
    url: 'https://github.com/yourusername'
  },
  {
    platform: 'LinkedIn',
    icon: 'fab fa-linkedin',
    url: 'https://linkedin.com/in/yourusername'
  },
  {
    platform: 'Twitter',
    icon: 'fab fa-twitter',
    url: 'https://twitter.com/yourusername'
  }
]
</script>

<template>
  <div class="contact-container">
    <h1>Contact</h1>
    <div class="contact-content">
      <div class="contact-info">
        <h2>Get in Touch</h2>
        <div class="info-item">
          <i class="fas fa-envelope"></i>
          <span>{{ contactInfo.email }}</span>
        </div>
        <div class="info-item">
          <i class="fab fa-weixin"></i>
          <span>{{ contactInfo.wechat }}</span>
        </div>
        <div class="info-item">
          <i class="fas fa-map-marker-alt"></i>
          <span>{{ contactInfo.location }}</span>
        </div>
      </div>

      <div class="social-links">
        <h2>Connect with Me</h2>
        <div class="social-grid">
          <a v-for="(social, index) in socialLinks" 
             :key="index" 
             :href="social.url" 
             class="social-item"
             target="_blank">
            <i :class="social.icon"></i>
            <span>{{ social.platform }}</span>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.contact-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

h1 {
  color: #2c3e50;
  margin-bottom: 2rem;
  text-align: center;
}

.contact-content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 3rem;
  margin-top: 2rem;
}

.contact-info, .social-links {
  background: #f8f9fa;
  padding: 2rem;
  border-radius: 8px;
}

h2 {
  color: #2c3e50;
  margin-bottom: 1.5rem;
}

.info-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1rem;
  color: #666;
}

.info-item i {
  font-size: 1.2rem;
  color: #42b983;
}

.social-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 1rem;
}

.social-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  padding: 1rem;
  background: white;
  border-radius: 8px;
  text-decoration: none;
  color: #2c3e50;
  transition: transform 0.3s ease;
}

.social-item:hover {
  transform: translateY(-5px);
}

.social-item i {
  font-size: 2rem;
  color: #42b983;
}

.social-item span {
  font-size: 0.9rem;
}
</style> 
<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'
import photo1 from '@/assets/images/photo1.jpg'
import photo2 from '@/assets/images/photo2.jpg'
import photo3 from '@/assets/images/photo3.jpg'
import photo4 from '@/assets/images/photo4.jpg'
import photo5 from '@/assets/images/photo5.jpg'
import photo6 from '@/assets/images/photo6.jpg'
import photo7 from '@/assets/images/photo7.jpg'
import photo8 from '@/assets/images/photo8.jpg'
import photo9 from '@/assets/images/photo9.jpg'
import link1 from '@/assets/images/link1.jpg'
import link2 from '@/assets/images/link2.png'
import link3 from '@/assets/images/link3.jpeg'
import link4 from '@/assets/images/link4.jpg'

const router = useRouter()

const socialLinks = [
  {
    icon: 'fab fa-github',
    url: 'https://github.com/dzbao'
  },
  {
    icon: 'fas fa-graduation-cap',
    url: 'https://scholar.google.com/citations?user=njTpYWsAAAAJ'
  },
  {
    icon: 'fab fa-weixin',
    showQrCode: true
  },
  {
    icon: 'fas fa-envelope',
    url: 'mailto:dzbao@zju.edu.cn'
  }
]

const skills = [
  { name: 'Python', level: 95 },
  { name: 'AI', level: 90 },
  { name: 'miniProgram', level: 85 },
  // { name: 'Machine Learning', level: 88 },
  // { name: 'Data Mining', level: 92 }
]

const projects = ref([])
const publications = ref([])
const showModal = ref(false)
const currentModal = ref(null)
const showQrCode = ref(false)

const loadProjects = async () => {
  try {
    const response = await fetch('/data/projects.json')
    const data = await response.json()
    projects.value = data.projects
  } catch (error) {
    console.error('Error loading projects:', error)
  }
}

const loadPublications = async () => {
  try {
    const response = await fetch('/data/publications.json')
    const data = await response.json()
    publications.value = data.publications
  } catch (error) {
    console.error('Error loading publications:', error)
  }
}

const gallery = [
  {
    image: photo1,
    title: 'Graduate',
    story: 'Zhejiang University<br>2023<br>Seeking Truth, Pursuing Innovation'
  },
  {
    image: photo2,
    title: 'Universal Studios',
    story: 'Peking<br>2024<br>One-day Wizard'
  },
  {
    image: photo3,
    title: 'Jingshan Temple',
    story: 'Hang Zhou<br>2025<br>Serenity'
  },
  {
    image: photo4,
    title: 'Qizhen Lake',
    story: 'Zhejiang University<br>2023<br>Leisure Time'
  },
  {
    image: photo5,
    title: 'Fenghuang Ancient Town',
    story: 'Hunan<br>2024<br>Happiness'
  },
  {
    image: photo6,
    title: 'Volleyball Game',
    story: 'Zhejiang University<br>2023<br>Collaboration'
  },
  {
    image: photo7,
    title: 'CUHK',
    story: 'Hong Kong<br>2023<br>Unity of Nature and Man'
  },
  {
    image: photo8,
    title: 'Zhu Hai',
    story: 'Guangdong<br>2023<br>The Sun and Moon Shell'
  },
  {
    image: photo9,
    title: 'Changbai Mountain',
    story: 'Jilin<br>2023<br>Tianchi Lake'
  }
]

const links = [
  link1, link2, link3, link4
]

const friendlyLinks = [
  {
    image: link1,
    name: 'Yang Yang',
    url: 'https://yangy.org'
  },
  {
    image: link2,
    name: 'Daoze Zhang',
    url: 'https://daozezhang.github.io/'
  },
  {
    image: link3,
    name: 'Xuanwen Huang',
    url: 'https://scholar.google.com/citations?user=JFLCWNQAAAAJ'
  },
  {
    image: link4,
    name: 'Junru Chen',
    url: 'https://mrnobodycali.github.io/'
  }
]

onMounted(() => {
  animateSkills()
  loadProjects()
  loadPublications()
})

const animateSkills = () => {
  const bars = document.querySelectorAll('.skill-progress')
  bars.forEach(bar => {
    const width = bar.getAttribute('data-level')
    bar.style.width = width + '%'
  })
}

const handleTagClick = (tag) => {
  if (tag.type === 'cite') {
    currentModal.value = tag.modal
    showModal.value = true
  } else {
    window.open(tag.url, '_blank')
  }
}

const closeModal = () => {
  showModal.value = false
  currentModal.value = null
}

const handleSocialClick = (social, event) => {
  if (social.showQrCode) {
    event.preventDefault()
    showQrCode.value = true
  }
}

const closeQrCode = () => {
  showQrCode.value = false
}

const navigateToDetail = (publication) => {
  if (publication.md) {
    router.push(`/publications/${publication.md}`)
  }
}
</script>

<template>
  <div class="home-container">
    <section class="banner">
      <div class="banner-overlay">
        <div class="banner-content">
          <h1>Hello, I'm Dezheng Bao</h1>
          <p class="intro-text">
            I am a Ph.D. student from <a href="http://www.cs.zju.edu.cn/" target="_blank" rel="noopener noreferrer">the College of Computer Science and Technology</a>, <a href="http://www.zju.edu.cn/" target="_blank" rel="noopener noreferrer">Zhejiang University</a>. My advisor is <a href="http://yangy.org/" target="_blank" rel="noopener noreferrer">Yang Yang</a>. My research interests include LLMs’ applications in specific domains and data mining. If you are interested in communicating or just chatting, please feel free to contact me.
          </p>
          <div class="social-links">
            <a v-for="(social, index) in socialLinks" 
               :key="index" 
               :href="social.url" 
               class="social-icon"
               :class="{ 'no-link': social.showQrCode }"
               target="_blank"
               @click="social.showQrCode ? handleSocialClick(social, $event) : null">
              <i :class="social.icon"></i>
            </a>
          </div>
          <div class="scroll-btn">
            <a href="#about" class="btn-primary">About Me</a>
          </div>
        </div>
      </div>
      <div class="scroll-indicator">
        <div class="mouse"></div>
      </div>
    </section>

    <section id="about" class="about-section">
      <div class="container">
        <h2>About Me</h2>
        <div class="about-content">
          <div class="about-image">
            <img src="@/assets/images/avatar.jpg" alt="Profile Photo" />
          </div>
          <div class="about-info">
            <div class="about-text">
              <p>
                Welcome! I'm Dezheng Bao( 包德政 ), a Ph.D. student from <a href="http://www.cs.zju.edu.cn/" target="_blank" rel="noopener noreferrer">the College of Computer Science and Technology</a>, <a href="http://www.zju.edu.cn/" target="_blank" rel="noopener noreferrer">Zhejiang University</a>. My advisor is <a href="http://yangy.org/" target="_blank" rel="noopener noreferrer">Yang Yang</a>. 
              </p>
              <p>
                I’ve got my bachelor degree of Computer Science while minoring in <a href="http://www.cec.zju.edu.cn/" target="_blank" rel="noopener noreferrer">Finance</a> as outstanding graduate in Zhejiang University. 
              </p>
            </div>
            <div class="about-grid">
              <div class="interests-section">
                <h3>Interests</h3>
                <ul class="interests-list">
                  <li>Large Language Models</li>
                  <li>Data Mining</li>
                </ul>
              </div>
              
              <div class="education-section">
                <h3>Education</h3>
                <div class="education-items">
                  <div class="education-item">
                    <h4>Ph.D. in Artificial Intelligence</h4>
                    <p class="year">2023 - Now</p>
                    <p class="school">Zhejiang University</p>
                  </div>
                  <div class="education-item">
                    <h4>BEng in Computer Science</h4>
                    <p class="year">2019 - 2023</p>
                    <p class="school">Zhejiang University</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="content-section">
      <div class="grid-container">
        <!-- <div class="skills-section">
          <h2>Technical Expertise</h2>
          <div class="skills-container">
            <div v-for="skill in skills" :key="skill.name" class="skill-item">
              <div class="skill-info">
                <span class="skill-name">{{ skill.name }}</span>
                <span class="skill-percentage">{{ skill.level }}%</span>
              </div>
              <div class="skill-bar">
                <div class="skill-progress" :data-level="skill.level"></div>
              </div>
            </div>
          </div>
        </div> -->

        <div class="featured-publications">
          <h2>Featured Publications</h2>
          <div class="publications-grid">
            <div 
              v-for="pub in publications" 
              :key="pub.title" 
              class="publication-card"
              @click="navigateToDetail(pub)"
            >
              <h3>{{ pub.title }}</h3>
              <p class="authors">{{ pub.authors }}</p>
              <p class="conference">{{ pub.conference }}</p>
              <div class="tags">
                <button 
                  v-for="(tag, tagIndex) in pub.tags" 
                  :key="tagIndex"
                  class="tag"
                  :style="{
                    color: tag.color,
                    backgroundColor: tag.backgroundColor
                  }"
                  @click.stop="handleTagClick(tag)"
                >
                  <i :class="tag.icon"></i>
                  {{ tag.label }}
                </button>
              </div>
            </div>
          </div>
        </div>

        <div class="gallery-section">
          <h2>Life Moments</h2>
          <div class="gallery-grid">
            <div v-for="(photo, index) in gallery" 
                 :key="index" 
                 class="gallery-item"
                 :style="{ backgroundImage: `url(${photo.image})` }">
              <div class="gallery-overlay">
                <h3>{{ photo.title }}</h3>
                <p v-html="photo.story"></p>
              </div>
            </div>
          </div>
        </div>

        <!-- <div class="featured-projects">
          <h2>Featured Projects</h2>
          <div class="projects-grid">
            <div v-for="project in projects" :key="project.title" class="project-card">
              <h3>{{ project.title }}</h3>
              <p>{{ project.description }}</p>
              <div class="tech-tags">
                <span v-for="tech in project.tech" :key="tech" class="tech-tag">
                  {{ tech }}
                </span>
              </div>
              <a :href="project.link" target="_blank" class="project-link">View Project</a>
            </div>
          </div>
        </div> -->

        <div class="contact-section">
          <h2>Contact Me</h2>
          <div class="contact-content">
            <p class="poem">飞光，飞光，劝尔一杯酒</p>
            <div class="contact-info">
              <a href="mailto:dzbao@zju.edu.cn" class="email">
                <i class="fas fa-envelope"></i>
                dzbao@zju.edu.cn
              </a>
              <div class="address">
                <i class="fas fa-map-marker-alt"></i>
                <p>Caoguangbiao Main Building, Yuquan Campus, Zhejiang University, Hangzhou, Zhejiang Province 310027</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Modal -->
    <div v-if="showModal" class="modal-overlay" @click="closeModal">
      <div class="modal-content" @click.stop>
        <h3>{{ currentModal?.title }}</h3>
        <pre>{{ currentModal?.content }}</pre>
        <button 
          class="close-button"
          :style="{ backgroundColor: currentModal?.buttonColor }"
          @click="closeModal"
        >
          {{ currentModal?.buttonText }}
        </button>
      </div>
    </div>

    <!-- QR Code Modal -->
    <div v-if="showQrCode" class="modal-overlay" @click="closeQrCode">
      <div class="modal-content qrcode-modal" @click.stop>
        <h3>WeChat QRcode</h3>
        <div class="qrcode-container">
          <img src="@/assets/images/qrcode.jpg" alt="QR Code" />
        </div>
        <button 
          class="close-button"
          style="backgroundColor: #64ffda"
          @click="closeQrCode"
        >
          关闭
        </button>
      </div>
    </div>

    <!-- 友情链接部分 -->
    <div class="friendly-links section">
      <div class="container">
        <h2>Friendly Links</h2>
        <div class="links-grid">
          <a 
            v-for="(link, index) in friendlyLinks" 
            :key="index"
            :href="link.url"
            target="_blank"
            rel="noopener noreferrer"
            class="link-item"
          >
            <div class="link-image">
              <img :src="link.image" :alt="link.name" />
            </div>
            <p class="link-name">{{ link.name }}</p>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.home-container {
  width: 100%;
  background-color: #0a192f;
  color: #e6f1ff;
}

.banner {
  position: relative;
  height: 100vh;
  background: linear-gradient(135deg, #0a192f 0%, #112240 100%);
  overflow: hidden;
}

.banner::before {
  content: '';
  position: absolute;
  width: 200%;
  height: 200%;
  background: radial-gradient(
    circle,
    rgba(100, 255, 218, 0.15) 0%,
    rgba(136, 162, 255, 0.15) 25%,
    rgba(100, 255, 218, 0.1) 50%,
    rgba(10, 25, 47, 0) 75%
  );
  animation: rotate 30s linear infinite;
  transform-origin: center center;
}

.banner::after {
  content: '';
  position: absolute;
  width: 150%;
  height: 150%;
  background: radial-gradient(
    circle,
    rgba(136, 162, 255, 0.1) 0%,
    rgba(100, 255, 218, 0.1) 30%,
    rgba(10, 25, 47, 0) 60%
  );
  animation: rotate 20s linear infinite reverse;
  transform-origin: center center;
}

@keyframes rotate {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.banner-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 2rem;
  z-index: 1;
}

.banner-content {
  max-width: 800px;
  text-align: center;
}

.banner-content h1 {
  font-size: 4rem;
  margin-bottom: 1.5rem;
  font-weight: 600;
  background: linear-gradient(120deg, #64ffda, #88a2ff);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.intro-text {
  font-size: 1.2rem;
  line-height: 1.8;
  color: #8892b0;
  margin-bottom: 2rem;
}

.button-group {
  display: flex;
  gap: 1rem;
  justify-content: center;
  margin-bottom: 2rem;
}

.btn-primary {
  padding: 0.8rem 2rem;
  background-color: transparent;
  border: 2px solid #64ffda;
  color: #64ffda;
  text-decoration: none;
  border-radius: 4px;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.btn-primary::before {
  content: '';
  opacity: 0;
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: rgba(100,255,218,0.1);
  transition: transform 0.3s ease;
}

.btn-primary:hover::before {
  opacity: 1;
  transform: translateX(100%);
}

.social-links {
  display: flex;
  gap: 1.5rem;
  justify-content: center;
}

.social-icon {
  color: #64ffda;
  font-size: 1.5rem;
  transition: all 0.3s ease;
}

.social-icon:hover {
  transform: translateY(-3px);
  color: #88a2ff;
}

.social-icon.no-link {
  cursor: pointer;
}

.social-icon.no-link:hover {
  transform: translateY(-3px);
  color: #88a2ff;
}

.scroll-indicator {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
}

.mouse {
  width: 26px;
  height: 40px;
  border: 2px solid #64ffda;
  border-radius: 20px;
  position: relative;
}

.mouse::before {
  content: '';
  width: 4px;
  height: 8px;
  background: #64ffda;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  top: 6px;
  border-radius: 2px;
  animation: scroll 2s infinite;
}

@keyframes scroll {
  0% { transform: translate(-50%, 0); opacity: 1; }
  100% { transform: translate(-50%, 20px); opacity: 0; }
}

.content-section {
  background-color: #112240;
  padding: 2rem 0;
}

.grid-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.skills-section {
  margin-bottom: 4rem;
}

h2 {
  color: #64ffda;
  margin-bottom: 2rem;
  font-size: 2rem;
  position: relative;
}

h2::after {
  content: '';
  position: absolute;
  bottom: -0.5rem;
  left: 0;
  width: 60px;
  height: 4px;
  background: linear-gradient(90deg, #64ffda, transparent);
}

.skills-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.skill-item {
  background: rgba(255,255,255,0.05);
  padding: 1.5rem;
  border-radius: 8px;
  backdrop-filter: blur(10px);
}

.skill-info {
  display: flex;
  justify-content: space-between;
  margin-bottom: 0.5rem;
}

.skill-name {
  color: #ccd6f6;
}

.skill-percentage {
  color: #64ffda;
}

.skill-bar {
  height: 6px;
  background: rgba(255,255,255,0.1);
  border-radius: 3px;
  overflow: hidden;
}

.skill-progress {
  height: 100%;
  background: linear-gradient(90deg, #64ffda, #88a2ff);
  width: 0;
  transition: width 1s ease;
}

.gallery-section {
  margin-top: 4rem;
  margin-bottom: 4rem;
}

.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
  margin-top: 2rem;
}

.gallery-item {
  position: relative;
  height: 280px;
  background-size: cover;
  background-position: center;
  border-radius: 12px;
  overflow: hidden;
  cursor: pointer;
}

.gallery-item::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(
    to bottom,
    rgba(10, 25, 47, 0.2),
    rgba(10, 25, 47, 0.8)
  );
  opacity: 0;
  transition: opacity 0.3s ease;
}

.gallery-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 2rem;
  transform: translateY(100%);
  transition: transform 0.3s ease;
  background: linear-gradient(
    to top,
    rgba(10, 25, 47, 0.9),
    rgba(10, 25, 47, 0.7)
  );
  color: #e6f1ff;
}

.gallery-item:hover::before {
  opacity: 1;
}

.gallery-item:hover .gallery-overlay {
  transform: translateY(0);
}

.gallery-overlay h3 {
  color: #64ffda;
  margin-bottom: 0.5rem;
  font-size: 1.2rem;
}

.gallery-overlay p {
  color: #8892b0;
  font-size: 0.9rem;
  line-height: 1.6;
}

.gallery-item {
  transform: scale(1);
  transition: transform 0.3s ease;
}

.gallery-item:hover {
  transform: scale(1.02);
}

.gallery-overlay h3,
.gallery-overlay p {
  opacity: 0;
  transform: translateY(10px);
  transition: all 0.3s ease;
}

.gallery-item:hover .gallery-overlay h3,
.gallery-item:hover .gallery-overlay p {
  opacity: 1;
  transform: translateY(0);
}

.gallery-item:hover .gallery-overlay h3 {
  transition-delay: 0.1s;
}

.gallery-item:hover .gallery-overlay p {
  transition-delay: 0.2s;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.project-card {
  background: rgba(255, 255, 255, 0.05);
  padding: 2rem;
  border-radius: 8px;
  backdrop-filter: blur(10px);
  transition: transform 0.3s ease;
}

.project-card:hover {
  transform: translateY(-5px);
}

.project-card h3 {
  color: #ccd6f6;
  margin-bottom: 1rem;
}

.project-card p {
  color: #8892b0;
  margin-bottom: 1.5rem;
}

.project-link {
  display: inline-block;
  margin-top: 1rem;
  color: #64ffda;
  text-decoration: none;
  transition: color 0.3s ease;
}

.project-link:hover {
  color: #88a2ff;
}

.tech-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-top: 1rem;
}

.tech-tag {
  background: rgba(100, 255, 218, 0.1);
  color: #64ffda;
  padding: 0.25rem 0.75rem;
  border-radius: 4px;
  font-size: 0.875rem;
}

.featured-publications {
  margin-top: 4rem;
}

.publications-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  margin-top: 2rem;
}

.publication-card {
  background: rgba(255, 255, 255, 0.05);
  padding: 2rem;
  border-radius: 8px;
  backdrop-filter: blur(10px);
  transition: transform 0.3s ease;
  cursor: pointer;
}

.publication-card:hover {
  transform: translateY(-5px);
}

.publication-card h3 {
  color: #64ffda;
  margin-bottom: 1rem;
}

.authors {
  color: #8892b0;
  margin-bottom: 0.5rem;
  font-size: 0.9rem;
}

.conference {
  color: #ccd6f6;
  margin-bottom: 1rem;
  font-size: 0.9rem;
}

.tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tag {
  padding: 0.25rem 0.75rem;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.3s ease;
  border: none;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.875rem;
}

.tag:hover {
  transform: translateY(-2px);
  opacity: 0.8;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-content {
  background: #112240;
  padding: 2rem;
  border-radius: 8px;
  max-width: 600px;
  width: 90%;
}

.modal-content h3 {
  color: #64ffda;
  margin-bottom: 1rem;
}

.modal-content pre {
  background: rgba(0, 0, 0, 0.2);
  padding: 1rem;
  border-radius: 4px;
  overflow-x: auto;
  color: #8892b0;
}

.close-button {
  margin-top: 1rem;
  padding: 0.5rem 1rem;
  color: #0a192f;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.close-button:hover {
  opacity: 0.8;
}

.contact-section {
  margin-top: 4rem;
  padding: 2rem;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 8px;
  backdrop-filter: blur(10px);
}

.contact-content {
  max-width: 800px;
  margin: 0 auto;
  text-align: center;
}

.poem {
  font-size: 1.5rem;
  color: #64ffda;
  margin-bottom: 2rem;
  font-style: italic;
}

.contact-info {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  align-items: center;
}

.email {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #ccd6f6;
  text-decoration: none;
  font-size: 1.1rem;
  transition: all 0.3s ease;
}

.email:hover {
  color: #64ffda;
  transform: translateY(-2px);
}

.address {
  display: flex;
  align-items: flex-start;
  gap: 0.5rem;
  color: #8892b0;
  max-width: 600px;
  line-height: 1.6;
}

.address i {
  margin-top: 0.3rem;
  color: #64ffda;
}

@media (max-width: 768px) {
  .banner-content h1 {
    font-size: 3rem;
  }
  
  .intro-text {
    font-size: 1rem;
  }
  
  .grid-container {
    padding: 0 1rem;
  }
  
  .gallery-grid {
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  }
  
  .gallery-item {
    height: 250px;
  }
  
  .gallery-overlay {
    padding: 1.5rem;
  }
  
  .poem {
    font-size: 1.2rem;
  }
  
  .email {
    font-size: 1rem;
  }
  
  .address {
    font-size: 0.9rem;
  }
}

/* 友情链接样式 */
.friendly-links {
  background-color: #0a192f;
  padding-bottom: 5rem;
}

.links-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 2rem;
  justify-items: center;
}

.link-item {
  text-align: center;
  transition: transform 0.3s ease;
  text-decoration: none;
  cursor: pointer;
}

.link-item:hover {
  transform: translateY(-10px);
}

.link-image {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  overflow: hidden;
  margin: 0 auto 1rem;
  border: 3px solid #64ffda;
}

.link-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.link-name {
  color: #ccd6f6;
  font-size: 1.1rem;
}

@media (max-width: 768px) {
  .links-grid {
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  }
  
  .link-image {
    width: 100px;
    height: 100px;
  }
}

.qrcode-modal {
  text-align: center;
}

.qrcode-container {
  margin: 2rem auto;
  max-width: 200px;
}

.qrcode-container img {
  width: 100%;
  height: auto;
  border: 4px solid #64ffda;
  border-radius: 8px;
}

.profile-section {
  display: flex;
  align-items: center;
  gap: 3rem;
  margin-bottom: 2rem;
}

.profile-image {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  overflow: hidden;
  border: 4px solid #64ffda;
  flex-shrink: 0;
}

.profile-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.profile-info {
  text-align: left;
}

.about-section {
  background-color: #112240;
  padding: 6rem 0;
  position: relative;
}

.about-content {
  display: flex;
  gap: 4rem;
  align-items: flex-start;
  margin-top: 3rem;
}

.about-image {
  flex: 0 0 300px;
  position: relative;
}

.about-image::after {
  content: '';
  position: absolute;
  top: 15px;
  left: 15px;
  right: -15px;
  bottom: -15px;
  border: 2px solid #64ffda;
  border-radius: 4px;
  z-index: 0;
}

.about-image img {
  width: 100%;
  border-radius: 4px;
  position: relative;
  z-index: 1;
  filter: grayscale(20%);
  transition: all 0.3s ease;
}

.about-image:hover img {
  filter: none;
  transform: translate(-5px, -5px);
}

.about-info {
  flex: 1;
}

.about-text {
  margin-bottom: 2rem;
}

.about-text p {
  color: #8892b0;
  font-size: 1.1rem;
  line-height: 1.8;
  margin-bottom: 1rem;
}

.about-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 3rem;
}

.interests-section h3,
.education-section h3 {
  color: #64ffda;
  font-size: 1.5rem;
  margin-bottom: 1.5rem;
}

.education-item h4 {
  color: #ccd6f6;
  font-size: 1.1rem;
  margin-bottom: 0.5rem;
}

@media (max-width: 1024px) {
  .about-content {
    flex-direction: column;
    align-items: center;
    gap: 3rem;
  }

  .about-image {
    flex: 0 0 250px;
  }

  .about-info {
    text-align: center;
  }

  .about-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .interests-list {
    justify-content: center;
  }
}

@media (max-width: 768px) {
  .about-image {
    flex: 0 0 200px;
  }

  .about-text p {
    font-size: 1rem;
  }

  .interests-section h3,
  .education-section h3 {
    font-size: 1.3rem;
  }
}

.scroll-btn {
  margin-top: 2rem;
}

.scroll-btn .btn-primary {
  font-size: 1.1rem;
  padding: 1rem 2rem;
}
</style>

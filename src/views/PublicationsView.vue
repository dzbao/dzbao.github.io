<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const publications = ref([])
const showModal = ref(false)
const currentModal = ref(null)
const loading = ref(true)

const loadPublications = async () => {
  try {
    const response = await fetch('/data/publications.json')
    const data = await response.json()
    publications.value = data.publications
  } catch (error) {
    console.error('Error loading publications:', error)
  } finally {
    loading.value = false
  }
}

const navigateToDetail = (mdId) => {
  router.push(`/publications/${mdId}`)
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

onMounted(() => {
  loadPublications()
})
</script>

<template>
  <div class="publications-container">
    <h1>Publications</h1>
    
    <div class="publications-list">
      <div 
        v-for="(pub, index) in publications" 
        :key="index" 
        class="publication-card"
        @click="navigateToDetail(pub.md)"
      >
        <div class="publication-content">
          <h2>{{ pub.title }}</h2>
          <p class="authors">{{ pub.authors }}</p>
          <p class="conference">{{ pub.conference }}</p>
        </div>
        <div class="tags">
          <button 
            v-for="(tag, tagIndex) in pub.tags" 
            :key="tagIndex"
            class="tag"
            :style="{
              color: tag.color,
              backgroundColor: tag.backgroundColor
            }"
            @click.stop="tag.type === 'cite' ? showModal(tag.modal) : window.open(tag.url, '_blank')"
          >
            <i :class="tag.icon"></i>
            {{ tag.label }}
          </button>
        </div>
      </div>
    </div>

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
  </div>
</template>

<style scoped>
.publications-container {
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

.publications-list {
  display: grid;
  gap: 2rem;
}

.publication-card {
  background: rgba(255, 255, 255, 0.05);
  padding: 2rem;
  border-radius: 8px;
  backdrop-filter: blur(10px);
  transition: transform 0.3s ease;
}

.publication-card:hover {
  transform: translateY(-5px);
}

.publication-card h2 {
  color: #64ffda;
  margin-bottom: 1rem;
  font-size: 1.5rem;
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

@media (max-width: 768px) {
  .publications-container {
    padding: 6rem 1rem 1rem;
  }
  
  .publication-card {
    padding: 1.5rem;
  }
}
</style> 
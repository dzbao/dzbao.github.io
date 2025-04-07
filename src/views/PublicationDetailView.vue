<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import MarkdownIt from 'markdown-it'
import hljs from 'highlight.js'
import 'highlight.js/styles/github-dark.css'

const route = useRoute()
const md = new MarkdownIt({
  html: true,
  linkify: true,
  typographer: true,
  highlight: function (str, lang) {
    if (lang && hljs.getLanguage(lang)) {
      try {
        return hljs.highlight(str, { language: lang }).value
      } catch (__) {}
    }
    return ''
  }
})

const publication = ref(null)
const content = ref('')
const loading = ref(true)

const loadPublication = async () => {
  try {
    // 加载 publications.json
    const response = await fetch('/data/publications.json')
    const data = await response.json()
    const pub = data.publications.find(p => p.md === route.params.id)
    
    if (pub) {
      publication.value = pub
      // 加载对应的 MD 文件
      const mdResponse = await fetch(`/md/${pub.md}`)
      const mdContent = await mdResponse.text()
      content.value = md.render(mdContent)
    }
  } catch (error) {
    console.error('Error loading publication:', error)
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  loadPublication()
})
</script>

<template>
  <div class="publication-detail">
    <div v-if="loading" class="loading">
      <div class="spinner"></div>
    </div>
    
    <div v-else-if="publication" class="content">
      <div class="header">
        <h1>{{ publication.title }}</h1>
        <div class="meta">
          <p class="authors">{{ publication.authors }}</p>
          <p class="conference">{{ publication.conference }}</p>
        </div>
      </div>
      
      <div class="markdown-content" v-html="content"></div>
      
      <div class="tags">
        <button 
          v-for="(tag, index) in publication.tags" 
          :key="index"
          class="tag"
          :style="{
            color: tag.color,
            backgroundColor: tag.backgroundColor
          }"
          @click="tag.type === 'cite' ? showModal(tag.modal) : window.open(tag.url, '_blank')"
        >
          <i :class="tag.icon"></i>
          {{ tag.label }}
        </button>
      </div>
    </div>
    
    <div v-else class="not-found">
      <h2>Publication not found</h2>
    </div>
  </div>
</template>

<style scoped>
.publication-detail {
  max-width: 1200px;
  margin: 0 auto;
  padding: 6rem 2rem 2rem;
  min-height: 100vh;
  background-color: #0a192f;
  color: #e6f1ff;
}

.loading {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 50vh;
}

.spinner {
  width: 40px;
  height: 40px;
  border: 4px solid #64ffda;
  border-top-color: transparent;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

.header {
  margin-bottom: 3rem;
}

.header h1 {
  color: #64ffda;
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

.meta {
  color: #8892b0;
}

.meta p {
  margin-bottom: 0.5rem;
}

.markdown-content {
  background: rgba(255, 255, 255, 0.05);
  padding: 2rem;
  border-radius: 8px;
  backdrop-filter: blur(10px);
  margin-bottom: 2rem;
}

.markdown-content :deep(h1) {
  color: #64ffda;
  margin: 2rem 0 1rem;
}

.markdown-content :deep(h2) {
  color: #64ffda;
  margin: 1.5rem 0 1rem;
}

.markdown-content :deep(p) {
  color: #ccd6f6;
  line-height: 1.6;
  margin-bottom: 1rem;
}

.markdown-content :deep(code) {
  background: rgba(0, 0, 0, 0.2);
  padding: 0.2rem 0.4rem;
  border-radius: 4px;
  font-family: monospace;
}

.markdown-content :deep(pre) {
  background: rgba(0, 0, 0, 0.2);
  padding: 1rem;
  border-radius: 8px;
  overflow-x: auto;
  margin: 1rem 0;
}

.markdown-content :deep(a) {
  color: #64ffda;
  text-decoration: none;
  transition: color 0.3s ease;
}

.markdown-content :deep(a:hover) {
  color: #88a2ff;
}

.tags {
  display: flex;
  gap: 1rem;
  margin-top: 2rem;
}

.tag {
  padding: 0.5rem 1rem;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.3s ease;
  border: none;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.tag:hover {
  transform: translateY(-2px);
  opacity: 0.8;
}

.not-found {
  text-align: center;
  padding: 4rem 0;
}

.not-found h2 {
  color: #64ffda;
  font-size: 2rem;
}

@media (max-width: 768px) {
  .publication-detail {
    padding: 6rem 1rem 1rem;
  }
  
  .header h1 {
    font-size: 2rem;
  }
  
  .markdown-content {
    padding: 1.5rem;
  }
}
</style> 
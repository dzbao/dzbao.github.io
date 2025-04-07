<script setup>
const photos = [
  {
    image: '@/assets/gallery/photo1.jpg',
    title: 'Photo 1',
    description: 'Description for photo 1'
  },
  {
    image: '@/assets/gallery/photo2.jpg',
    title: 'Photo 2',
    description: 'Description for photo 2'
  },
  {
    image: '@/assets/gallery/photo3.jpg',
    title: 'Photo 3',
    description: 'Description for photo 3'
  },
  {
    image: '@/assets/gallery/photo4.jpg',
    title: 'Photo 4',
    description: 'Description for photo 4'
  }
]
</script>

<template>
  <div class="gallery-container">
    <h1>Gallery</h1>
    <div class="photo-grid">
      <div v-for="(photo, index) in photos" :key="index" class="photo-item">
        <div class="photo-wrapper">
          <img :src="photo.image" :alt="photo.title">
          <div class="photo-overlay">
            <h3>{{ photo.title }}</h3>
            <p>{{ photo.description }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.gallery-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

h1 {
  color: #2c3e50;
  margin-bottom: 2rem;
  text-align: center;
}

.photo-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
}

.photo-item {
  aspect-ratio: 1;
  overflow: hidden;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.photo-wrapper {
  position: relative;
  width: 100%;
  height: 100%;
}

.photo-wrapper img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.photo-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 2rem;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.photo-overlay h3 {
  color: white;
  margin-bottom: 1rem;
  transform: translateY(20px);
  transition: transform 0.3s ease;
}

.photo-overlay p {
  color: rgba(255, 255, 255, 0.8);
  text-align: center;
  transform: translateY(20px);
  transition: transform 0.3s ease;
}

.photo-item:hover .photo-wrapper img {
  transform: scale(1.1);
}

.photo-item:hover .photo-overlay {
  opacity: 1;
}

.photo-item:hover .photo-overlay h3,
.photo-item:hover .photo-overlay p {
  transform: translateY(0);
}
</style> 
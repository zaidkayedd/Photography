<template>
  <div class="min-h-screen" v-if="categoryData">
    <!-- Hero Section -->
    <section class="section-padding bg-gradient-to-br from-neutral-900 to-neutral-800 text-white">
      <div class="container-custom">
        <div class="text-center">
          <router-link 
            to="/portfolio" 
            class="inline-flex items-center text-primary-400 hover:text-primary-300 transition-colors mb-8 animate-fade-in"
          >
            <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 20 20">
              <path fill-rule="evenodd" d="M9.707 16.707a1 1 0 01-1.414 0l-6-6a1 1 0 010-1.414l6-6a1 1 0 011.414 1.414L5.414 9H17a1 1 0 110 2H5.414l4.293 4.293a1 1 0 010 1.414z" clip-rule="evenodd"/>
            </svg>
            Back to Portfolio
          </router-link>
          <h1 class="mb-8 animate-slide-up text-white">{{ categoryData.title }}</h1>
          <div class="w-24 h-1 bg-gradient-to-r from-primary-500 to-primary-600 mx-auto mb-8"></div>
          <p class="text-xl text-neutral-300 max-w-3xl mx-auto animate-slide-up animation-delay-200 leading-relaxed">
            {{ categoryData.description }}
          </p>
        </div>
      </div>
    </section>

    <!-- Gallery Section -->
    <section class="section-padding">
      <div class="container-custom">
        <!-- Filter Options -->
        <div class="flex flex-wrap justify-center gap-4 mb-16">
          <button
            v-for="filter in filters"
            :key="filter"
            @click="activeFilter = filter"
            :class="[
              'px-6 py-3 rounded-full font-medium transition-all duration-300',
              activeFilter === filter
                ? 'bg-neutral-900 text-white shadow-medium'
                : 'bg-neutral-100 text-neutral-700 hover:bg-neutral-200'
            ]"
          >
            {{ filter }}
          </button>
        </div>

        <!-- Photo Grid -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div
            v-for="(photo, index) in filteredPhotos"
            :key="index"
            class="group cursor-pointer animate-scale-in"
            :style="{ animationDelay: `${index * 100}ms` }"
            @click="openLightbox(index)"
          >
            <div class="card-elevated overflow-hidden">
              <div class="relative aspect-square overflow-hidden">
                <img
                  :src="photo.thumbnail"
                  :alt="photo.title"
                  class="w-full h-full object-cover transition-all duration-500 group-hover:scale-110"
                  loading="lazy"
                />
                <div class="absolute inset-0 bg-black/0 group-hover:bg-black/20 transition-all duration-300 flex items-center justify-center">
                  <div class="w-16 h-16 bg-white/20 backdrop-blur-sm rounded-full flex items-center justify-center opacity-0 group-hover:opacity-100 transition-all duration-300 transform scale-75 group-hover:scale-100">
                    <svg class="w-8 h-8 text-white" fill="currentColor" viewBox="0 0 20 20">
                      <path d="M10 12a2 2 0 100-4 2 2 0 000 4z"/>
                      <path fill-rule="evenodd" d="M.458 10C1.732 5.943 5.522 3 10 3s8.268 2.943 9.542 7c-1.274 4.057-5.064 7-9.542 7S1.732 14.057.458 10zM14 10a4 4 0 11-8 0 4 4 0 018 0z" clip-rule="evenodd"/>
                    </svg>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Lightbox -->
    <div
      v-if="lightboxOpen"
      class="fixed inset-0 z-50 bg-black/95 backdrop-blur-sm flex items-center justify-center p-4"
      @click="closeLightbox"
    >
      <div class="relative max-w-6xl max-h-full">
        <img
          :src="filteredPhotos[currentPhotoIndex].fullSize"
          :alt="filteredPhotos[currentPhotoIndex].title"
          class="max-w-full max-h-full object-contain rounded-lg shadow-large"
          @click.stop
        />
        
        <!-- Navigation Buttons -->
        <button
          v-if="currentPhotoIndex > 0"
          @click.stop="previousPhoto"
          class="absolute left-4 top-1/2 transform -translate-y-1/2 w-12 h-12 bg-white/20 backdrop-blur-sm rounded-full flex items-center justify-center text-white hover:bg-white/30 transition-all duration-200"
        >
          <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 20 20">
            <path fill-rule="evenodd" d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z" clip-rule="evenodd"/>
          </svg>
        </button>
        
        <button
          v-if="currentPhotoIndex < filteredPhotos.length - 1"
          @click.stop="nextPhoto"
          class="absolute right-4 top-1/2 transform -translate-y-1/2 w-12 h-12 bg-white/20 backdrop-blur-sm rounded-full flex items-center justify-center text-white hover:bg-white/30 transition-all duration-200"
        >
          <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 20 20">
            <path fill-rule="evenodd" d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z" clip-rule="evenodd"/>
          </svg>
        </button>

        <!-- Close Button -->
        <button
          @click.stop="closeLightbox"
          class="absolute top-4 right-4 w-12 h-12 bg-white/20 backdrop-blur-sm rounded-full flex items-center justify-center text-white hover:bg-white/30 transition-all duration-200"
        >
          <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 20 20">
            <path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd"/>
          </svg>
        </button>

        <!-- Photo Info -->
        <div class="absolute bottom-4 left-4 bg-white/20 backdrop-blur-sm rounded-xl p-4 text-white">
          <h3 class="text-lg font-semibold mb-1">{{ filteredPhotos[currentPhotoIndex].title }}</h3>
          <p class="text-sm text-neutral-300">{{ currentPhotoIndex + 1 }} of {{ filteredPhotos.length }}</p>
        </div>
      </div>
    </div>

    <!-- CTA Section -->
    <section class="section-padding bg-neutral-50">
      <div class="container-custom text-center">
        <h2 class="mb-6">Inspired by What You See?</h2>
        <p class="text-xl text-neutral-600 max-w-2xl mx-auto mb-12 leading-relaxed">
          Let's create something beautiful together. Contact us to discuss your photography needs.
        </p>
        <router-link to="/contact" class="btn-primary text-lg px-10 py-5">
          <span>Get in Touch</span>
          <svg class="w-5 h-5 ml-2" fill="currentColor" viewBox="0 0 20 20">
            <path fill-rule="evenodd" d="M10.293 3.293a1 1 0 011.414 0l6 6a1 1 0 010 1.414l-6 6a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-4.293-4.293a1 1 0 010-1.414z" clip-rule="evenodd"/>
          </svg>
        </router-link>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted, onUnmounted } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const category = route.params.category as string

const activeFilter = ref('All')
const lightboxOpen = ref(false)
const currentPhotoIndex = ref(0)

// Mock data for different categories
const portfolioData: Record<string, any> = {
  weddings: {
    title: 'Wedding Photography',
    description: 'Romantic and timeless wedding photography capturing love stories that will be cherished forever',
    filters: ['All', 'Ceremony', 'Reception', 'Portraits', 'Details'],
    photos: [
      { title: 'Ceremony Kiss', filter: 'Ceremony', thumbnail: 'https://images.pexels.com/photos/1024993/pexels-photo-1024993.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/1024993/pexels-photo-1024993.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Wedding Rings', filter: 'Details', thumbnail: 'https://images.pexels.com/photos/265722/pexels-photo-265722.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/265722/pexels-photo-265722.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'First Dance', filter: 'Reception', thumbnail: 'https://images.pexels.com/photos/1024967/pexels-photo-1024967.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/1024967/pexels-photo-1024967.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Bride Portrait', filter: 'Portraits', thumbnail: 'https://images.pexels.com/photos/1454818/pexels-photo-1454818.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/1454818/pexels-photo-1454818.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Wedding Bouquet', filter: 'Details', thumbnail: 'https://images.pexels.com/photos/1729797/pexels-photo-1729797.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/1729797/pexels-photo-1729797.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Reception Party', filter: 'Reception', thumbnail: 'https://images.pexels.com/photos/1024978/pexels-photo-1024978.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/1024978/pexels-photo-1024978.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' }
    ]
  },
  automotive: {
    title: 'Automotive Photography',
    description: 'Dynamic automotive photography showcasing vehicles with artistic flair and technical precision',
    filters: ['All', 'Classic Cars', 'Sports Cars', 'Motorcycles', 'Details'],
    photos: [
      { title: 'Classic Muscle Car', filter: 'Classic Cars', thumbnail: 'https://images.pexels.com/photos/164634/pexels-photo-164634.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/164634/pexels-photo-164634.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Sports Car Detail', filter: 'Details', thumbnail: 'https://images.pexels.com/photos/358070/pexels-photo-358070.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/358070/pexels-photo-358070.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Vintage Motorcycle', filter: 'Motorcycles', thumbnail: 'https://images.pexels.com/photos/104842/bmw-vehicle-ride-bike-104842.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/104842/bmw-vehicle-ride-bike-104842.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Racing Car', filter: 'Sports Cars', thumbnail: 'https://images.pexels.com/photos/100650/pexels-photo-100650.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/100650/pexels-photo-100650.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Engine Detail', filter: 'Details', thumbnail: 'https://images.pexels.com/photos/279949/pexels-photo-279949.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/279949/pexels-photo-279949.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Classic Convertible', filter: 'Classic Cars', thumbnail: 'https://images.pexels.com/photos/120049/pexels-photo-120049.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/120049/pexels-photo-120049.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' }
    ]
  },
  graduations: {
    title: 'Graduation Photography',
    description: 'Celebrating academic achievements and milestone moments with pride and joy',
    filters: ['All', 'Individual', 'Family', 'Ceremony', 'Group'],
    photos: [
      { title: 'Graduate Portrait', filter: 'Individual', thumbnail: 'https://images.pexels.com/photos/267885/pexels-photo-267885.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/267885/pexels-photo-267885.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Family Celebration', filter: 'Family', thumbnail: 'https://images.pexels.com/photos/1205651/pexels-photo-1205651.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/1205651/pexels-photo-1205651.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Graduation Ceremony', filter: 'Ceremony', thumbnail: 'https://images.pexels.com/photos/267885/pexels-photo-267885.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/267885/pexels-photo-267885.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Class Group Photo', filter: 'Group', thumbnail: 'https://images.pexels.com/photos/1205651/pexels-photo-1205651.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/1205651/pexels-photo-1205651.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' }
    ]
  },
  portraits: {
    title: 'Portrait Photography',
    description: 'Professional portraits that capture personality, character, and the essence of who you are',
    filters: ['All', 'Headshots', 'Family', 'Children', 'Seniors'],
    photos: [
      { title: 'Professional Headshot', filter: 'Headshots', thumbnail: 'https://images.pexels.com/photos/1545743/pexels-photo-1545743.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/1545743/pexels-photo-1545743.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Family Portrait', filter: 'Family', thumbnail: 'https://images.pexels.com/photos/1128318/pexels-photo-1128318.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/1128318/pexels-photo-1128318.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Child Portrait', filter: 'Children', thumbnail: 'https://images.pexels.com/photos/1127000/pexels-photo-1127000.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/1127000/pexels-photo-1127000.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Senior Portrait', filter: 'Seniors', thumbnail: 'https://images.pexels.com/photos/1239291/pexels-photo-1239291.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/1239291/pexels-photo-1239291.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' }
    ]
  },
  architecture: {
    title: 'Architecture Photography',
    description: 'Architectural photography highlighting design, structure, and the beauty of built environments',
    filters: ['All', 'Modern', 'Historic', 'Interior', 'Details'],
    photos: [
      { title: 'Modern Building', filter: 'Modern', thumbnail: 'https://images.pexels.com/photos/323780/pexels-photo-323780.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/323780/pexels-photo-323780.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Historic Cathedral', filter: 'Historic', thumbnail: 'https://images.pexels.com/photos/356966/pexels-photo-356966.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/356966/pexels-photo-356966.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Interior Design', filter: 'Interior', thumbnail: 'https://images.pexels.com/photos/1571460/pexels-photo-1571460.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/1571460/pexels-photo-1571460.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Architectural Detail', filter: 'Details', thumbnail: 'https://images.pexels.com/photos/161758/governor-mansion-montgomery-alabama-grand-staircase-161758.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/161758/governor-mansion-montgomery-alabama-grand-staircase-161758.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' }
    ]
  },
  events: {
    title: 'Event Photography',
    description: 'Corporate and social events captured with professional expertise and creative vision',
    filters: ['All', 'Corporate', 'Social', 'Conferences', 'Parties'],
    photos: [
      { title: 'Corporate Event', filter: 'Corporate', thumbnail: 'https://images.pexels.com/photos/1190298/pexels-photo-1190298.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/1190298/pexels-photo-1190298.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Conference Speaker', filter: 'Conferences', thumbnail: 'https://images.pexels.com/photos/1181406/pexels-photo-1181406.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/1181406/pexels-photo-1181406.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Birthday Party', filter: 'Parties', thumbnail: 'https://images.pexels.com/photos/1729797/pexels-photo-1729797.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/1729797/pexels-photo-1729797.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' },
      { title: 'Social Gathering', filter: 'Social', thumbnail: 'https://images.pexels.com/photos/1024967/pexels-photo-1024967.jpeg?auto=compress&cs=tinysrgb&w=400&h=400&dpr=1', fullSize: 'https://images.pexels.com/photos/1024967/pexels-photo-1024967.jpeg?auto=compress&cs=tinysrgb&w=1200&h=800&dpr=1' }
    ]
  }
}

const categoryData = computed(() => portfolioData[category])
const filters = computed(() => categoryData.value?.filters || ['All'])

const filteredPhotos = computed(() => {
  if (!categoryData.value) return []
  if (activeFilter.value === 'All') {
    return categoryData.value.photos
  }
  return categoryData.value.photos.filter((photo: any) => photo.filter === activeFilter.value)
})

const openLightbox = (index: number) => {
  currentPhotoIndex.value = index
  lightboxOpen.value = true
  document.body.style.overflow = 'hidden'
}

const closeLightbox = () => {
  lightboxOpen.value = false
  document.body.style.overflow = 'auto'
}

const nextPhoto = () => {
  if (currentPhotoIndex.value < filteredPhotos.value.length - 1) {
    currentPhotoIndex.value++
  }
}

const previousPhoto = () => {
  if (currentPhotoIndex.value > 0) {
    currentPhotoIndex.value--
  }
}

const handleKeyDown = (event: KeyboardEvent) => {
  if (!lightboxOpen.value) return
  
  switch (event.key) {
    case 'Escape':
      closeLightbox()
      break
    case 'ArrowRight':
      nextPhoto()
      break
    case 'ArrowLeft':
      previousPhoto()
      break
  }
}

onMounted(() => {
  document.addEventListener('keydown', handleKeyDown)
})

onUnmounted(() => {
  document.removeEventListener('keydown', handleKeyDown)
})
</script>
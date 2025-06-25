<template>
  <div class="min-h-screen">
    <!-- Hero Section -->
    <section class="section-padding bg-gradient-to-br from-neutral-900 to-neutral-800 text-white">
      <div class="container-custom text-center">
        <h1 class="mb-8 animate-fade-in text-white">Our Portfolio</h1>
        <div class="w-24 h-1 bg-gradient-to-r from-primary-500 to-primary-600 mx-auto mb-8"></div>
        <p class="text-xl text-neutral-300 max-w-3xl mx-auto animate-slide-up animation-delay-200 leading-relaxed">
          Explore our diverse collection of photography showcasing different styles, emotions, and unforgettable moments
        </p>
      </div>
    </section>

    <!-- Portfolio Categories -->
    <section class="section-padding relative">
      <div class="Portfolio"></div>
      <div class="container-custom">
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div
            v-for="(category, index) in portfolioCategories"
            :key="index"
            class="group cursor-pointer animate-scale-in"
            :style="{ animationDelay: `${index * 150}ms` }"
            @click="$router.push(`/portfolio/${category.slug}`)"
          >
            <div class="card-elevated overflow-hidden">
              <div class="relative aspect-[4/5] overflow-hidden">
                <img
                  :src="category.coverImage"
                  :alt="category.title"
                  class="w-full h-full object-cover transition-all duration-700 group-hover:scale-110"
                />
                <div class="absolute inset-0 bg-gradient-to-t from-black/90 via-black/20 to-transparent"></div>
                <div class="absolute inset-0 bg-primary-500/0 group-hover:bg-primary-500/10 transition-all duration-500"></div>
                
                <!-- Category Badge -->
                <div class="absolute top-6 left-6">
                  <span class="px-4 py-2 bg-white/20 backdrop-blur-sm rounded-full text-white text-sm font-medium">
                    {{ category.count }} photos
                  </span>
                </div>
              </div>
              
              <div class=" p-8 text-black">
                <h3 class="text-2xl font-bold mb-3 transform translate-y-2 group-hover:translate-y-0 transition-transform duration-500">
                  {{ category.title }}
                </h3>
                <p class="text-black mb-4 opacity-0 group-hover:opacity-100 transform translate-y-4 group-hover:translate-y-0 transition-all duration-500 delay-100 leading-relaxed">
                  {{ category.description }}
                </p>
                <div class="flex items-center opacity-0 group-hover:opacity-100 transform translate-y-4 group-hover:translate-y-0 transition-all duration-500 delay-200">
                  <span class="text-sm font-medium">Explore Collection</span>
                  <svg class="w-5 h-5 ml-2 transform group-hover:translate-x-1 transition-transform duration-300" fill="currentColor" viewBox="0 0 20 20">
                    <path fill-rule="evenodd" d="M10.293 3.293a1 1 0 011.414 0l6 6a1 1 0 010 1.414l-6 6a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-4.293-4.293a1 1 0 010-1.414z" clip-rule="evenodd"/>
                  </svg>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Call to Action -->
    <section class="section-padding bg-neutral-50 relative">
      <DotLottieVue  autoplay loop src="https://lottie.host/98e72703-525a-46a5-844e-d4611050d73c/SU1EG6cdki.lottie" class=" opacity-0 sm:opacity-[1] absolute right-0 top-[19rem] lg:top-14 w-[200px] 2xl:w-[500px] h-[200px] 2xl:h-[500px]" />

      <div class="container-custom text-center">
        <div class="max-w-4xl mx-auto">
          <h2 class="mb-6">Ready to Create Something Beautiful?</h2>
          <p class="text-xl text-neutral-600 mb-12 leading-relaxed">
            Let's discuss your photography needs and create stunning images that capture your unique story and vision.
          </p>
          <router-link to="/contact" class="btn-primary text-lg px-10 py-5 rounded-[10px]">
            <span>Get in Touch</span>
            <svg class="w-5 h-5 ml-2" fill="currentColor" viewBox="0 0 20 20">
              <path fill-rule="evenodd" d="M10.293 3.293a1 1 0 011.414 0l6 6a1 1 0 010 1.414l-6 6a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-4.293-4.293a1 1 0 010-1.414z" clip-rule="evenodd"/>
            </svg>
          </router-link>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup >
import { DotLottieVue } from '@lottiefiles/dotlottie-vue'

const portfolioCategories = [
  {
    title: 'Weddings',
    slug: 'weddings',
    description: 'Romantic and timeless wedding photography capturing love stories that will be cherished forever',
    coverImage: 'https://images.pexels.com/photos/1024993/pexels-photo-1024993.jpeg?auto=compress&cs=tinysrgb&w=800&h=1000&dpr=1',
    count: 120
  },
  {
    title: 'Automotive',
    slug: 'automotive',
    description: 'Dynamic automotive photography showcasing vehicles with artistic flair and technical precision',
    coverImage: 'https://images.pexels.com/photos/164634/pexels-photo-164634.jpeg?auto=compress&cs=tinysrgb&w=800&h=1000&dpr=1',
    count: 85
  },
  {
    title: 'Graduations',
    slug: 'graduations',
    description: 'Celebrating academic achievements and milestone moments with pride and joy',
    coverImage: 'https://images.pexels.com/photos/267885/pexels-photo-267885.jpeg?auto=compress&cs=tinysrgb&w=800&h=1000&dpr=1',
    count: 95
  },
  {
    title: 'Portraits',
    slug: 'portraits',
    description: 'Professional portraits that capture personality, character, and the essence of who you are',
    coverImage: 'https://images.pexels.com/photos/1545743/pexels-photo-1545743.jpeg?auto=compress&cs=tinysrgb&w=800&h=1000&dpr=1',
    count: 150
  },
  {
    title: 'Architecture',
    slug: 'architecture',
    description: 'Architectural photography highlighting design, structure, and the beauty of built environments',
    coverImage: 'https://images.pexels.com/photos/323780/pexels-photo-323780.jpeg?auto=compress&cs=tinysrgb&w=800&h=1000&dpr=1',
    count: 65
  },
  {
    title: 'Events',
    slug: 'events',
    description: 'Corporate and social events captured with professional expertise and creative vision',
    coverImage: 'https://images.pexels.com/photos/1190298/pexels-photo-1190298.jpeg?auto=compress&cs=tinysrgb&w=800&h=1000&dpr=1',
    count: 110
  }
]
</script>
<style scoped>
.Portfolio{
  width: 100%;
  height: 100%;
  position: absolute;
left: -80%;
  background-image: url(../assets/Circle1.png);
  background-repeat: no-repeat;
  background-position: 100% ;
background-size: contain;
z-index: 1; 
}
</style>
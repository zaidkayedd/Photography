<template>
  <div>
    <!-- Hero Section -->
    <section class="relative min-h-screen flex items-center justify-center overflow-hidden">
      <!-- Background Images -->
      <div class="absolute inset-0">
        <div
          v-for="(image, index) in heroImages"
          :key="index"
          :class="[
            'absolute inset-0 transition-all duration-3000 ease-in-out',
            currentImageIndex === index ? 'opacity-100 scale-100' : 'opacity-0 scale-110'
          ]"
        >
          <img
            :src="image.src"
            :alt="image.alt"
            class="w-full h-full object-cover"
          />
          <div class="absolute inset-0 bg-black/30"></div>
        </div>
      </div>

      <!-- Hero Content -->
      <div class="relative z-10 text-center text-white container-custom">
        <div class="max-w-5xl mx-auto">
          <div class="fade-in">
            <h1 class="mb-12 text-display font-normal tracking-tight">
              Visual
              <em class="font-light italic">Poetry</em>
            </h1>
          </div>
          <div class="slide-up stagger-2">
            <p class="text-xl md:text-2xl mb-16 text-white/90 font-light leading-relaxed max-w-3xl mx-auto">
              Where moments become memories and stories unfold through the lens of artistry
            </p>
          </div>
          <div class="slide-up stagger-3">
            <div class="flex flex-col sm:flex-row gap-6 justify-center">
              <router-link to="/portfolio" class="group inline-flex items-center px-12 py-5 border border-white/40 text-white hover:bg-white hover:text-black transition-all duration-500 tracking-loose">
                <span class="font-light">Explore Work</span>
                <svg class="w-4 h-4 ml-3 transform group-hover:translate-x-1 transition-transform duration-300" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M10.293 3.293a1 1 0 011.414 0l6 6a1 1 0 010 1.414l-6 6a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-4.293-4.293a1 1 0 010-1.414z" clip-rule="evenodd"/>
                </svg>
              </router-link>
              <router-link to="/contact" class="inline-flex items-center px-12 py-5 bg-white/10 backdrop-blur-sm text-white hover:bg-white hover:text-black transition-all duration-500 tracking-loose">
                <span class="font-light">Begin Your Story</span>
              </router-link>
            </div>
          </div>
        </div>
      </div>

      <!-- Navigation Dots -->
      <div class="absolute bottom-12 left-1/2 transform -translate-x-1/2 flex space-x-3">
        <button
          v-for="(image, index) in heroImages"
          :key="index"
          @click="currentImageIndex = index"
          :class="[
            'w-2 h-2 rounded-full transition-all duration-500',
            currentImageIndex === index 
              ? 'bg-white scale-125' 
              : 'bg-white/50 hover:bg-white/75'
          ]"
        ></button>
      </div>

      <!-- Scroll Indicator -->
      <div class="absolute bottom-12 right-12 text-white/60 hidden lg:block">
        <div class="flex flex-col items-center space-y-2">
          <div class="w-px h-16 bg-white/30"></div>
          <span class="text-xs font-light tracking-loose rotate-90 origin-center whitespace-nowrap">Scroll</span>
        </div>
      </div>
    </section>

    <!-- Featured Work Section -->
    <section class="section-padding selectedWorks">
      <div class="container-custom">
        <div class="text-center mb-24">
          <div class="fade-in">
            <h2 class="text-display mb-8">Selected Works</h2>
            <div class="divider mb-8"></div>
            <p class="text-lg text-neutral-600 font-light max-w-2xl mx-auto leading-relaxed">
              A curated collection of moments captured with intention, emotion, and artistic vision
            </p>
          </div>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-2">
          <div
            v-for="(work, index) in featuredWork"
            :key="index"
            class="group cursor-pointer overflow-hidden slide-up"
            :class="`stagger-${index + 1}`"
            @click="$router.push(`/portfolio/${work.category.toLowerCase()}`)"
          >
            <div class="relative aspect-[4/5] overflow-hidden bg-neutral-100">
              <img
                :src="work.image"
                :alt="work.title"
                class="w-full h-full object-cover card-hover"
              />
              <div class="image-overlay">
                <div class="absolute bottom-8 left-8 right-8 text-white transform translate-y-4 group-hover:translate-y-0 transition-transform duration-700">
                  <h3 class="text-display text-2xl mb-2">{{ work.title }}</h3>
                  <p class="text-white/80 font-light tracking-wide">{{ work.category }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Philosophy Section -->
    <section class="section-padding bg-neutral-50 relative ">
      <div class="Philosophy"></div>
      <div class="container-custom">
        <div class="max-w-4xl mx-auto text-center">
          <div class="fade-in">
            <h2 class="text-display mb-8">Our Philosophy</h2>
            <div class="divider mb-12"></div>
            <p class="text-2xl md:text-3xl text-neutral-700 font-light leading-relaxed mb-12 text-display">
              "Every photograph is a story waiting to be told, a moment suspended in time, 
              a memory preserved for eternity."
            </p>
            <p class="text-lg text-neutral-600 font-light leading-relaxed">
              We believe in the power of authentic storytelling through imagery. Our approach combines 
              technical mastery with emotional intelligence, creating photographs that not only document 
              moments but elevate them into art.
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Services Section -->
    <!-- <section class="section-padding  relative">
  <div class="Services"></div>
      <div class="container-custom">
        <div class="text-center mb-10">
          <div class="fade-in">
            <h2 class="text-display mb-8">Services</h2>
            <div class="divider mb-8"></div>
            <p class="text-lg text-neutral-600 font-light max-w-2xl mx-auto leading-relaxed">
              Comprehensive photography services tailored to capture your unique story
            </p>
          </div>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-16">
          <div
            v-for="(service, index) in services"
            :key="index"
            class="text-center slide-up "
            :class="`stagger-${index + 1}`"
          >
            <div class=" w-[400px] h-[300px] border-[1px] border-black rounded-[6px] p-2 flex items-center justify-center flex-col relative bg-opacity-[0.6]">
              <div class="w-16 h-px bg-black mx-auto  absolute top-[5%]"></div>
              <h3 class="text-display text-2xl mb-4 text-black font-[600]">{{ service.title }}</h3>
              <p class="text-neutral-600 font-light leading-relaxed">{{ service.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </section> -->

    <!-- Testimonial Section -->
    <section class="section-padding bg-black text-white">
      <div class="container-custom">
        <div class="max-w-4xl mx-auto text-center">
          <div class="fade-in">
            <blockquote class="text-3xl md:text-4xl text-display font-light leading-relaxed mb-12 italic">
              "Their ability to capture not just images, but emotions and stories, 
              is truly extraordinary. Every photograph tells a story."
            </blockquote>
            <div class="divider-light mb-8"></div>
            <cite class="text-white/70 font-light tracking-wide">Sarah & Michael Johnson</cite>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA Section -->
    <section class="section-padding">
      <div class="container-custom text-center">
        <div class="max-w-3xl mx-auto">
          <div class="fade-in">
            <h2 class="text-display mb-8">Begin Your Story</h2>
            <div class="divider mb-12"></div>
            <p class="text-xl text-neutral-600 font-light mb-16 leading-relaxed">
              Ready to create something extraordinary together? Let's discuss your vision 
              and craft images that will be treasured for generations.
            </p>
            <router-link to="/contact" class="btn-primary rounded-[10px]">
              <span>Start a Conversation</span>
            </router-link>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const currentImageIndex = ref(0)
let imageInterval: number | null = null

const heroImages = [
  {
    src: 'https://images.pexels.com/photos/1024993/pexels-photo-1024993.jpeg?auto=compress&cs=tinysrgb&w=1920&h=1080&dpr=1',
    alt: 'Wedding Photography'
  },
  {
    src: 'https://images.pexels.com/photos/1545743/pexels-photo-1545743.jpeg?auto=compress&cs=tinysrgb&w=1920&h=1080&dpr=1',
    alt: 'Portrait Photography'
  },
  {
    src: 'https://images.pexels.com/photos/164634/pexels-photo-164634.jpeg?auto=compress&cs=tinysrgb&w=1920&h=1080&dpr=1',
    alt: 'Automotive Photography'
  },
  {
    src: 'https://images.pexels.com/photos/323780/pexels-photo-323780.jpeg?auto=compress&cs=tinysrgb&w=1920&h=1080&dpr=1',
    alt: 'Architecture Photography'
  }
]

const featuredWork = [
  {
    title: 'Baja 2025',
    category: 'Automotive',
    image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT2cA_pv8mWImykbHjA1qIPJwZDNLl_uNV-EA&s'
  },
  {
    title: '911',
    category: 'Automotive',
    image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQo9eS7lu-Mab97UJ78_DNpGWbSSfKBBJOB6w&s'
  },
  {
    title: 'Mercedes',
    category: 'Automotive',
    image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcROo9fhaRtkN-eItqerrwpnYxb9A6AjLihOEw&s'
  },
  {
    title: 'Wadi Rum',
    category: 'Architecture',
    image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcToDpvWNYtYqKHhnJ4GB2VK1emQz1350cyi2APqFUrXNz5gAnWe16OVz0zLFKKFEXFU3p4&usqp=CAU'
  },
  {
    title: 'Class of 2024',
    category: 'Graduations',
    image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSLgcv_Y7DkeqSYy0VhiyEfAcY8ulcH8JJ-PsjlmeBojvuZ6x6ronVW6KOaGYK3ArqbVoI&usqp=CAU'
  },
  {
    title: 'Corporate Summit',
    category: 'Events',
    image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQr8zdnncaY048f-Fn-n9DG7fknZHeLsZL6p0Wvr00TKvb1Yxpi5BnfipmVWcz5bS6LW00&usqp=CAU  '
  }
]

const services = [
  {
    title: 'Weddings',
    description: 'Timeless documentation of your most important day, capturing authentic emotions and precious moments with artistic elegance.'
  },
  {
    title: 'Portraits',
    description: 'Professional portraits that reveal personality and character through thoughtful composition, lighting, and genuine connection.'
  },
  {
    title: 'Events',
    description: 'Corporate and social gatherings documented with discretion, creativity, and an eye for meaningful moments.'
  },
  {
    title: 'Automotive',
    description: 'Dynamic vehicle photography showcasing design, craftsmanship, and engineering excellence through artistic vision.'
  },
  {
    title: 'Architecture',
    description: 'Architectural photography that highlights form, function, and the poetry of built environments and spaces.'
  },
  {
    title: 'Graduations',
    description: 'Milestone celebrations captured with pride and joy, documenting achievements and the beginning of new chapters.'
  }
]

onMounted(() => {
  imageInterval = setInterval(() => {
    currentImageIndex.value = (currentImageIndex.value + 1) % heroImages.length
  }, 10000)
})

onUnmounted(() => {
  if (imageInterval) {
    clearInterval(imageInterval)
  }
})
</script>
<style scoped>
.Services{
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
.Philosophy{
  width: 100%;
  height: 100%;
  position: absolute;
top: 0;
left: -85%;
  background-image: url(../assets/Circle1.png);
  background-repeat: no-repeat;
  background-position: 100% ;
background-size: contain;
z-index: 1; 
}
.selectedWorks{
  background-image: url(../assets/Background2.png);
  background-repeat: no-repeat;
  background-size: 2600px;
background-position: center;
}
</style>
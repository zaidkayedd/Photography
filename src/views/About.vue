<template>
  <div class="min-h-screen">
    <!-- Hero Section -->
    <section class="section-padding bg-gradient-to-br from-neutral-900 to-neutral-800 text-white">
      <div class="container-custom">
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">
          <div class="animate-slide-in-left">
            <h1 class="mb-8 text-white">About Mohammed Shaheen</h1>
            <p class="text-xl mb-12 text-neutral-300 leading-relaxed">
              With over a decade of experience capturing life's most precious moments, 
              we specialize in creating timeless images that tell your unique story with artistry and emotion.
            </p>
            <div class="space-y-6">
              <div v-for="(achievement, index) in achievements" :key="index" class="flex items-center animate-slide-up" :style="{ animationDelay: `${index * 200}ms` }">
                <div class="w-12 h-12 bg-gradient-to-br from-primary-500 to-primary-600 rounded-xl flex items-center justify-center mr-6 shadow-large">
                  <svg class="w-6 h-6 text-white" fill="currentColor" viewBox="0 0 20 20">
                    <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd"/>
                  </svg>
                </div>
                <span class="text-lg font-medium">{{ achievement }}</span>
              </div>
            </div>
          </div>
          <div class="animate-slide-in-right">
            <div class="relative">
              <img
                src="../assets/shaheen.jpg"
                alt="Photographer at work"
                class="rounded-2xl shadow-large"
              />
              <div class="absolute -bottom-6 -right-6 w-32 h-32 bg-gradient-to-br from-primary-500 to-primary-600 rounded-2xl opacity-20"></div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Story Section -->
    <section class="section-padding Services">
  
      <div class="container-custom">
        <div class="max-w-4xl mx-auto">
          <div class="text-center mb-20">
            <h2 class="mb-2 animate-fade-in">Our Story</h2>
            <div class="blackLine w-[300px] sm:w-[500px] h-1 bg-black mx-auto mb-8"></div>
          </div>
          
          <div class="prose prose-lg mx-auto text-neutral-600 space-y-8">
            <p class="text-xl leading-relaxed animate-slide-up">
              Captures by Shaheen began as a passion project in 2013, born from a deep love for capturing 
              the authentic emotions and fleeting moments that make life extraordinary. What started 
              as weekend photography sessions has evolved into a full-service studio dedicated to 
              preserving your most treasured memories.
            </p>
            
            <p class="text-lg leading-relaxed animate-slide-up animation-delay-200">
              Our approach combines technical expertise with artistic vision, ensuring that every 
              photograph not only documents a moment but elevates it into a work of art. We believe 
              that great photography is about more than just technical perfection – it's about 
              understanding people, emotions, and the stories that make each moment unique.
            </p>
            
            <p class="text-lg leading-relaxed animate-slide-up animation-delay-400">
              From intimate portraits to grand celebrations, architectural marvels to automotive 
              artistry, we bring the same level of passion and professionalism to every project. 
              Our goal is simple: to create images that you'll treasure for a lifetime and beyond.
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Services Section -->
    <section class="section-padding bg-neutral-50 relative">
      <img src="../assets/Camera.png" class="Camera absolute w-[300px] h-[300px] right-[0%] opacity-0 xl:opacity-[1] "/>
      <div class="container-custom">
        <div class="text-center mb-20">
          <h2 class="mb-6 animate-fade-in">Our Services</h2>
          <div class="orangeLine w-[300px] sm:w-[500px] h-1 mx-auto mb-8"></div>
          <p class="text-xl text-neutral-600 max-w-3xl mx-auto animate-slide-up animation-delay-200 leading-relaxed">
            Comprehensive photography services tailored to your unique needs and vision
          </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div
            v-for="(service, index) in services"
            :key="index"
            class="card p-8 hover:shadow-large transition-all duration-500 animate-scale-in"
            :style="{ animationDelay: `${index * 200}ms` }"
          >
            <div class="w-16 h-16 bg-gradient-to-br from-primary-500 to-primary-600 rounded-2xl flex items-center justify-center mb-6 shadow-medium">
              <svg class="w-8 h-8 text-white" fill="currentColor" viewBox="0 0 20 20" v-html="service.icon"></svg>
            </div>
            <h3 class="text-2xl font-[600] text-neutral-900 mb-4">{{ service.title }}</h3>
            <p class="text-neutral-600 mb-8 leading-relaxed">{{ service.description }}</p>
            <ul class="space-y-3">
              <li v-for="feature in service.features" :key="feature" class="flex items-center text-neutral-600">
                <div class="w-5 h-5 bg-primary-100 rounded-full flex items-center justify-center mr-3 flex-shrink-0">
                  <svg class="w-3 h-3 text-primary-600" fill="currentColor" viewBox="0 0 20 20">
                    <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd"/>
                  </svg>
                </div>
                {{ feature }}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA Section -->
    <section class="section-padding bg-gradient-to-br from-neutral-900 to-neutral-800 text-white">
      <div class="container-custom text-center">
        <h2 class="mb-6 text-white">Let's Create Something Amazing Together</h2>
        <p class="text-xl text-neutral-300 max-w-2xl mx-auto mb-12 leading-relaxed">
          Ready to capture your story? Get in touch and let's discuss how we can bring your vision to life.
        </p>
        <router-link to="/contact" class="btn-primary bg-primary-500 hover:bg-primary-600 text-lg px-10 py-5 rounded-[10px]">
          <span>Start Your Project</span>
          <svg class="w-5 h-5 ml-2" fill="currentColor" viewBox="0 0 20 20">
            <path fill-rule="evenodd" d="M10.293 3.293a1 1 0 011.414 0l6 6a1 1 0 010 1.414l-6 6a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-4.293-4.293a1 1 0 010-1.414z" clip-rule="evenodd"/>
          </svg>
        </router-link>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
const achievements = [
  '10+ Years of Professional Experience',
  '500+ Happy Clients Worldwide',
  'Award-Winning Photography',
  'Featured in Leading Publications'
]

const services = [
  {
    title: 'Wedding Photography',
    description: 'Capturing the magic and emotion of your special day with timeless elegance and artistic vision.',
    icon: '<path d="M3.172 5.172a4 4 0 015.656 0L10 6.343l1.172-1.171a4 4 0 115.656 5.656L10 17.657l-6.828-6.829a4 4 0 010-5.656z"/>',
    features: ['Full day coverage', 'Engagement sessions', 'Online gallery', 'Premium print packages']
  },
  {
    title: 'Portrait Photography',
    description: 'Professional portraits that capture your personality, character, and unique essence.',
    icon: '<path fill-rule="evenodd" d="M10 9a3 3 0 100-6 3 3 0 000 6zm-7 9a7 7 0 1114 0H3z" clip-rule="evenodd"/>',
    features: ['Studio sessions', 'Outdoor locations', 'Family portraits', 'Professional headshots']
  },
  {
    title: 'Event Photography',
    description: 'Documenting your corporate events, celebrations, and special gatherings with professional expertise.',
    icon: '<path d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"/>',
    features: ['Corporate events', 'Birthday celebrations', 'Graduations', 'Social gatherings']
  }
]
</script>
<style scoped>
.Services{
  width: 100%;
  height: 100%;
  background-image: url(../assets/background.png);
  background-repeat: no-repeat;
  background-position: center;
  background-size: contain;
  z-index: 1;
}
.card{
  box-shadow: 7px 7px 10px 0px #0000001A;
  border-radius: 10px;
  cursor: pointer;

}
.card:hover{
scale: 1.1;

}
img.Camera {
    -webkit-animation: mover 2s infinite  alternate;
    animation: mover 2s infinite  alternate;
    filter: drop-shadow(0 0 30px #F5B041); /* Adjust glow color */

}
img.Camera {
    -webkit-animation: mover 2s infinite  alternate;
    animation: mover 2s infinite  alternate;
}
@-webkit-keyframes mover {
    0% { transform: translateY(0); }
    100% { transform: translateY(-70px); }
}
@keyframes mover {
    0% { transform: translateY(0); }
    100% { transform: translateY(-70px); }
}
.orangeLine{
  box-shadow: 0px 5.26px 15.78px 0px rgba(230, 156, 43, 0.35);
background: linear-gradient(90deg, rgba(245, 176, 65, 0) 0%, rgba(245, 176, 65, 0.47) 50.72%, rgba(255, 203, 124, 0) 100%, rgba(230, 156, 43, 0) 100%);
}
.blackLine{
  box-shadow: 0px 6.26px 15.78px 0px black;

}
</style>
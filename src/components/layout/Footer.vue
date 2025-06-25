<template>
  <footer class="bg-neutral-900 text-white">
    <div class="container-custom p-[4rem]">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-16">
        <!-- Logo and Description -->
        <div class="lg:col-span-2">
          <h3 class="text-3xl text-display font-normal mb-4 tracking-wide">CapturesByShaheen</h3>
          <p class="text-white/70 font-light leading-relaxed mb-4 max-w-md text-lg">
            Capturing life's most precious moments with artistic vision, technical excellence, 
            and a deep understanding of human emotion.
          </p>
          <div class="flex space-x-4">
            <a 
              v-for="social in socialLinks" 
              :key="social.name"
              :href="social.href" 
              class="w-12 h-12 border border-white/20 hover:border-white/40 hover:bg-white/10 flex items-center justify-center transition-all duration-300 group"
            >
              <svg class="h-5 w-5 text-white/60 group-hover:text-white transition-colors duration-300" fill="currentColor" viewBox="0 0 24 24">
                <path :d="social.icon"/>
              </svg>
            </a>
          </div>
        </div>

        <!-- Navigation -->
        <div>
          <h4 class="text-lg font-light mb-4 tracking-wide">Navigation</h4>
          <ul class="space-y-2">
            <li v-for="link in quickLinks" :key="link.name">
              <router-link 
                :to="link.href" 
                class="text-white/70 hover:text-white font-light transition-colors duration-300 tracking-wide"
              >
                {{ link.name }}
              </router-link>
            </li>
          </ul>
        </div>

        <!-- Contact -->
        <div>
          <h4 class="text-lg font-light mb-4 tracking-wide">Contact</h4>
          <ul class="space-y-4">
            <li v-for="contact in contactInfo" :key="contact.type">
              <component 
                :is="contact.href ? 'a' : 'div'"
                :href="contact.href"
                class="text-white/70 hover:text-white font-light transition-colors duration-300 leading-relaxed"
                v-html="contact.content"
              />
            </li>
          </ul>
        </div>
      </div>

      <div class="mt-4 pt-12 border-t border-white/10">
        <div class="flex flex-col md:flex-row justify-between items-center">
          <p class="text-white/50 text-sm font-light tracking-wide">
            &copy; 2025 Developed By Zaid Kayed.
          </p>
    
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
const socialLinks = [
  {
    name: 'Instagram',
    href: '#',
    icon: 'M12.017 0C5.396 0 .029 5.367.029 11.987c0 5.079 3.158 9.417 7.618 11.174-.105-.949-.199-2.403.041-3.439.219-.937 1.406-5.957 1.406-5.957s-.359-.72-.359-1.781c0-1.663.967-2.911 2.168-2.911 1.024 0 1.518.769 1.518 1.688 0 1.029-.653 2.567-.992 3.992-.285 1.193.6 2.165 1.775 2.165 2.128 0 3.768-2.245 3.768-5.487 0-2.861-2.063-4.869-5.008-4.869-3.41 0-5.409 2.562-5.409 5.199 0 1.033.394 2.143.889 2.741.098.119.112.225.085.347-.09.375-.293 1.199-.334 1.363-.053.225-.172.271-.402.166-1.498-.69-2.436-2.888-2.436-4.649 0-3.785 2.75-7.262 7.929-7.262 4.163 0 7.398 2.967 7.398 6.931 0 4.136-2.607 7.464-6.227 7.464-1.216 0-2.357-.631-2.75-1.378l-.748 2.853c-.271 1.043-1.002 2.35-1.492 3.146C9.57 23.812 10.763 24.009 12.017 24.009c6.624 0 11.99-5.367 11.99-11.988C24.007 5.367 18.641.001 12.017.001z'
  },
  {
    name: 'Twitter',
    href: '#',
    icon: 'M24 4.557c-.883.392-1.832.656-2.828.775 1.017-.609 1.798-1.574 2.165-2.724-.951.564-2.005.974-3.127 1.195-.897-.957-2.178-1.555-3.594-1.555-3.179 0-5.515 2.966-4.797 6.045-4.091-.205-7.719-2.165-10.148-5.144-1.29 2.213-.669 5.108 1.523 6.574-.806-.026-1.566-.247-2.229-.616-.054 2.281 1.581 4.415 3.949 4.89-.693.188-1.452.232-2.224.084.626 1.956 2.444 3.379 4.6 3.419-2.07 1.623-4.678 2.348-7.29 2.04 2.179 1.397 4.768 2.212 7.548 2.212 9.142 0 14.307-7.721 13.995-14.646.962-.695 1.797-1.562 2.457-2.549z'
  },
  {
    name: 'Facebook',
    href: '#',
    icon: 'M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z'
  }
]

const quickLinks = [
  { name: 'Home', href: '/' },
  { name: 'About', href: '/about' },
  { name: 'Portfolio', href: '/portfolio' },
  { name: 'Contact', href: '/contact' },
]

const contactInfo = [

  {
    type: 'email',
    content: 'moh.shaheen187@gmail.com',
    href: 'moh.shaheen187@gmail.com'
  },
  {
    type: 'phone',
    content: '(962) 772165549',
    href: 'tel:+962772165549'
  }
]
</script>
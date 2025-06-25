<template>
  <header class="fixed top-0 left-0 right-0 z-50 transition-all duration-500" :class="headerClasses">
    <nav class="container-custom">
      <div class="flex justify-between items-center h-24">
        <!-- Logo -->
        <div class="flex-shrink-0">
          <router-link to="/" class="text-2xl text-display font-normal tracking-wide text-neutral-900 hover:text-neutral-600 transition-colors duration-300">
            CapturesByShaheen
          </router-link>
        </div>

        <!-- Desktop Navigation -->
        <div class="hidden md:block">
          <div class="flex items-center space-x-12">
            <router-link
              v-for="item in navigation"
              :key="item.name"
              :to="item.href"
              class="text-sm font-light text-neutral-600 hover:text-neutral-900 transition-colors duration-300 tracking-wide relative group"
              :class="[
                $route.path === item.href ? 'text-neutral-900' : ''
              ]"
            >
              {{ item.name }}
              <span class="absolute -bottom-1 left-0 w-0 h-px bg-neutral-900 transition-all duration-300 group-hover:w-full"></span>
            </router-link>
          </div>
        </div>

        <!-- Mobile menu button -->
        <div class="md:hidden">
          <button
            @click="toggleMobileMenu"
            class="p-2 text-neutral-600 hover:text-neutral-900 transition-colors duration-300"
          >
            <svg
              :class="{ hidden: mobileMenuOpen, block: !mobileMenuOpen }"
              class="h-6 w-6 transition-transform duration-300"
              stroke="currentColor"
              fill="none"
              viewBox="0 0 24 24"
            >
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M4 6h16M4 12h16M4 18h16" />
            </svg>
            <svg
              :class="{ block: mobileMenuOpen, hidden: !mobileMenuOpen }"
              class="h-6 w-6 transition-transform duration-300"
              stroke="currentColor"
              fill="none"
              viewBox="0 0 24 24"
            >
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
      </div>

      <!-- Mobile Navigation -->
      <div 
        :class="{ 
          'opacity-100 translate-y-0': mobileMenuOpen, 
          'opacity-0 -translate-y-4 pointer-events-none': !mobileMenuOpen 
        }" 
        class="md:hidden absolute top-full left-0 right-0 bg-white/95 backdrop-blur-md border-t border-neutral-200/50 transition-all duration-500"
      >
        <div class="container-custom py-8">
          <div class="space-y-6">
            <router-link
              v-for="item in navigation"
              :key="item.name"
              :to="item.href"
              @click="closeMobileMenu"
              class="block text-lg font-light text-neutral-600 hover:text-neutral-900 transition-colors duration-300 tracking-wide"
              :class="[
                $route.path === item.href ? 'text-neutral-900' : ''
              ]"
            >
              {{ item.name }}
            </router-link>
          </div>
        </div>
      </div>
    </nav>
  </header>
</template>

<script setup lang="ts">
import { ref, computed, onMounted, onUnmounted } from 'vue'

const mobileMenuOpen = ref(false)
const scrolled = ref(false)

const navigation = [
  { name: 'Home', href: '/' },
  { name: 'About', href: '/about' },
  { name: 'Portfolio', href: '/portfolio' },
  { name: 'Contact', href: '/contact' },
]

const headerClasses = computed(() => ({
  'bg-white/95 backdrop-blur-md shadow-sm': scrolled.value,
  'bg-transparent': !scrolled.value
}))

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value
}

const closeMobileMenu = () => {
  mobileMenuOpen.value = false
}

const handleScroll = () => {
  scrolled.value = window.scrollY > 50
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>
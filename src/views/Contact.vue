<template>
  <div class="min-h-screen">
    <!-- Hero Section -->
    <section class="section-padding bg-gradient-to-br from-neutral-900 to-neutral-800 text-white">
      <div class="container-custom text-center">
        <h1 class="mb-8 animate-fade-in text-white">Get In Touch</h1>
        <div class="w-24 h-1 bg-gradient-to-r from-primary-500 to-primary-600 mx-auto mb-8"></div>
        <p class="text-xl text-neutral-300 max-w-3xl mx-auto animate-slide-up animation-delay-200 leading-relaxed">
          Ready to capture your special moments? Let's discuss your photography needs and bring your vision to life.
        </p>
      </div>
    </section>

    <!-- Contact Section -->
    <section class="section-padding ">
      <div class="Contact"></div>
      <div class="container-custom">
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-20">
          <!-- Contact Information -->
          <div class="animate-slide-in-left">
            <h2 class="text-3xl font-bold text-neutral-900 mb-12">Contact Information</h2>
            
            <div class="space-y-10">
              <div v-for="(contact, index) in contactInfo" :key="index" class="flex items-start animate-slide-up" :style="{ animationDelay: `${index * 200}ms` }">
                <div class="w-14 h-14 bg-gradient-to-br from-primary-500 to-primary-600 rounded-2xl flex items-center justify-center mr-6 mt-1 shadow-medium flex-shrink-0">
                  <svg class="w-6 h-6 text-white" fill="currentColor" viewBox="0 0 20 20">
                    <path :d="contact.icon"/>
                  </svg>
                </div>
                <div>
                  <h3 class="text-xl font-semibold text-neutral-900 mb-3">{{ contact.title }}</h3>
                  <component 
                    :is="contact.href ? 'a' : 'div'"
                    :href="contact.href"
                    class="text-neutral-600 leading-relaxed hover:text-primary-600 transition-colors duration-200"
                    v-html="contact.content"
                  />
                </div>
              </div>
            </div>

            <!-- Business Hours Card -->
            <!-- <div class="card p-8 mt-12 animate-slide-up animation-delay-600">
              <h3 class="text-xl font-semibold text-neutral-900 mb-6">Business Hours</h3>
              <div class="space-y-3 text-neutral-600">
                <div class="flex justify-between">
                  <span>Monday - Friday</span>
                  <span class="font-medium">9:00 AM - 6:00 PM</span>
                </div>
                <div class="flex justify-between">
                  <span>Saturday</span>
                  <span class="font-medium">10:00 AM - 4:00 PM</span>
                </div>
                <div class="flex justify-between">
                  <span>Sunday</span>
                  <span class="font-medium">By appointment only</span>
                </div>
              </div>
            </div> -->
          </div>

          <!-- Contact Form -->
          <div class="animate-slide-in-right">
            <div class="card p-10">
              <h2 class="text-3xl font-bold text-neutral-900 mb-8">Send us a Message</h2>
              
              <form @submit.prevent="submitForm" class="space-y-8">
                <!-- Full Name -->
                <div>
                  <label for="fullName" class="block text-sm font-semibold text-neutral-700 mb-3">
                    Full Name *
                  </label>
                  <input
                    type="text"
                    id="fullName"
                    v-model="form.fullName"
                    required
                    class="w-full px-6 py-4 border-2 border-neutral-200 rounded-xl focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-all duration-200 text-neutral-900"
                    placeholder="Your full name"
                  />
                </div>

                <!-- Email -->
                <div>
                  <label for="email" class="block text-sm font-semibold text-neutral-700 mb-3">
                    Email Address *
                  </label>
                  <input
                    type="email"
                    id="email"
                    v-model="form.email"
                    required
                    class="w-full px-6 py-4 border-2 border-neutral-200 rounded-xl focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-all duration-200 text-neutral-900"
                    placeholder="your.email@example.com"
                  />
                </div>

                <!-- Phone -->
                <div>
                  <label for="phone" class="block text-sm font-semibold text-neutral-700 mb-3">
                    Phone Number
                  </label>
                  <input
                    type="tel"
                    id="phone"
                    v-model="form.phone"
                    class="w-full px-6 py-4 border-2 border-neutral-200 rounded-xl focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-all duration-200 text-neutral-900"
                    placeholder="(123) 456-7890"
                  />
                </div>

                <!-- Service Type -->
                <div>
                  <label for="serviceType" class="block text-sm font-semibold text-neutral-700 mb-3">
                    Service Type *
                  </label>
                  <select
                    id="serviceType"
                    v-model="form.serviceType"
                    required
                    class="w-full px-6 py-4 border-2 border-neutral-200 rounded-xl focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-all duration-200 text-neutral-900"
                  >
                    <option value="">Select a service</option>
                    <option value="wedding">Wedding Photography</option>
                    <option value="portrait">Portrait Photography</option>
                    <option value="event">Event Photography</option>
                    <option value="automotive">Automotive Photography</option>
                    <option value="graduation">Graduation Photography</option>
                    <option value="architecture">Architecture Photography</option>
                    <option value="other">Other</option>
                  </select>
                </div>

                <!-- Project Details -->
                <div>
                  <label for="projectDetails" class="block text-sm font-semibold text-neutral-700 mb-3">
                    Project Details *
                  </label>
                  <textarea
                    id="projectDetails"
                    v-model="form.projectDetails"
                    required
                    rows="6"
                    class="w-full px-6 py-4 border-2 border-neutral-200 rounded-xl focus:ring-2 focus:ring-primary-500 focus:border-primary-500 transition-all duration-200 resize-vertical text-neutral-900"
                    placeholder="Tell us about your photography needs, event details, preferred dates, and any specific requirements..."
                  ></textarea>
                </div>

                <!-- Submit Button -->
                <div>
                  <button
                    type="submit"
                    :disabled="isSubmitting"
                    class="w-full btn-primary text-lg py-5 disabled:opacity-50 disabled:cursor-not-allowed rounded-[10px]"
                  >
                    <span v-if="!isSubmitting" class="flex items-center justify-center">
                      Send Message
                      <svg class="w-5 h-5 ml-2" fill="currentColor" viewBox="0 0 20 20">
                        <path d="M2.003 5.884L10 9.882l7.997-3.998A2 2 0 0016 4H4a2 2 0 00-1.997 1.884zM18 8.118l-8 4-8-4V14a2 2 0 002 2h12a2 2 0 002-2V8.118z"/>
                      </svg>
                    </span>
                    <span v-else class="flex items-center justify-center">
                      <svg class="animate-spin -ml-1 mr-3 h-5 w-5" fill="none" viewBox="0 0 24 24">
                        <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                        <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                      </svg>
                      Sending...
                    </span>
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Success Modal -->
    <div
      v-if="showSuccessModal"
      class="fixed inset-0 z-50 bg-black/50 backdrop-blur-sm flex items-center justify-center p-4 "
      @click="showSuccessModal = false"
    >
      <div class="card p-10 max-w-md w-full text-center animate-scale-in bg-white rounded-[10px]" @click.stop>
        <div class="w-20 h-20 bg-gradient-to-br from-green-500 to-green-600 rounded-full flex items-center justify-center mx-auto mb-6 shadow-large">
          <svg class="w-10 h-10 text-white" fill="currentColor" viewBox="0 0 20 20">
            <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"/>
          </svg>
        </div>
        <h3 class="text-2xl font-extrabold text-neutral-900 mb-4">Message Sent Successfully!</h3>
        <p class="text-neutral-600 mb-8 leading-relaxed">
          Thank you for contacting us. We'll get back to you within 24 hours to discuss your photography needs.
        </p>
        <button
          @click="showSuccessModal = false"
          class="btn-primary rounded-[10px]"
        >
          Close
        </button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const isSubmitting = ref(false)
const showSuccessModal = ref(false)

const form = ref({
  fullName: '',
  email: '',
  phone: '',
  serviceType: '',
  projectDetails: ''
})

const contactInfo = [

  {
    title: 'Email',
    icon: 'M2.003 5.884L10 9.882l7.997-3.998A2 2 0 0016 4H4a2 2 0 00-1.997 1.884zM18 8.118l-8 4-8-4V14a2 2 0 002 2h12a2 2 0 002-2V8.118z',
    content: 'moh.shaheen187@gmail.com',
    href: 'moh.shaheen187@gmail.com'
  },
  {
    title: 'Phone',
    icon: 'M2 3a1 1 0 011-1h2.153a1 1 0 01.986.836l.74 4.435a1 1 0 01-.54 1.06l-1.548.773a11.037 11.037 0 006.105 6.105l.774-1.548a1 1 0 011.059-.54l4.435.74a1 1 0 01.836.986V17a1 1 0 01-1 1h-2C7.82 18 2 12.18 2 5V3z',
    content: '(962) 772165549',
    href: 'tel:+962772165549'
  }
]

const submitForm = async () => {
  isSubmitting.value = true
  
  // Simulate form submission
  await new Promise(resolve => setTimeout(resolve, 2000))
  
  // Reset form
  form.value = {
    fullName: '',
    email: '',
    phone: '',
    serviceType: '',
    projectDetails: ''
  }
  
  isSubmitting.value = false
  showSuccessModal.value = true
}
</script>
<style scoped>
.Contact{
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
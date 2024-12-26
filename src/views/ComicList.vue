<template>
  <div class="min-h-screen bg-gray-100 p-6">
    <div class="max-w-7xl mx-auto">
      <h1 class="text-3xl font-bold text-gray-900 mb-8">Comic Collection</h1>

      <!-- Loading State -->
      <div v-if="loading" class="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-6">
        <div v-for="i in 8" :key="i" class="bg-white rounded-lg shadow-md overflow-hidden">
          <div class="w-full h-48 bg-gray-200 animate-pulse"></div>
          <div class="p-4 space-y-3">
            <div class="h-4 bg-gray-200 rounded animate-pulse"></div>
            <div class="h-4 bg-gray-200 rounded animate-pulse w-2/3"></div>
            <div class="flex justify-between items-center pt-2">
              <div class="h-4 bg-gray-200 rounded animate-pulse w-1/4"></div>
              <div class="h-8 bg-gray-200 rounded animate-pulse w-1/3"></div>
            </div>
          </div>
        </div>
      </div>

      <!-- Error State -->
      <div v-else-if="error" class="bg-red-50 border border-red-200 rounded-md p-4">
        <div class="flex">
          <div class="flex-shrink-0">
            <svg class="h-5 w-5 text-red-400" viewBox="0 0 20 20" fill="currentColor">
              <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd" />
            </svg>
          </div>
          <div class="ml-3">
            <h3 class="text-sm font-medium text-red-800">Error loading comics</h3>
            <p class="text-sm text-red-700 mt-1">{{ error }}</p>
            <button 
              @click="fetchData" 
              class="mt-2 text-sm text-red-600 hover:text-red-500 font-medium"
            >
              Try again
            </button>
          </div>
        </div>
      </div>

      <!-- Comics Grid -->
      <div v-else class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
        <div 
          v-for="comic in filteredComics" 
          :key="comic.id" 
          class="bg-white rounded-lg shadow-md overflow-hidden hover:shadow-lg transition-shadow duration-300"
        >
          <div class="relative">
            <div v-if="comic.featured" class="absolute top-2 right-2 bg-yellow-400 text-xs px-2 py-1 rounded-full">
              Featured
            </div>
            <img 
              :src="comic.image || '/placeholder-comic.jpg'" 
              :alt="comic.title"
              class="w-full h-48 object-cover"
              @error="handleImageError"
            >
          </div>
          
          <div class="p-4">
            <h2 class="text-xl font-semibold text-gray-900 mb-2">{{ comic.title }}</h2>
            <p class="text-gray-600 text-sm mb-4 line-clamp-2">{{ comic.description }}</p>
            
            <div class="flex justify-between items-center">
              <span class="text-blue-600 font-bold">${{ comic.price || 'Free' }}</span>
              <div class="flex space-x-2">
                <router-link 
                  :to="{ name: 'comic-detail', params: { id: comic.id }}"
                  class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600"
                >
                  View
                </router-link>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'
import { useRoute } from 'vue-router'
import api from '../services/api'

const route = useRoute()
const comics = ref([])
const loading = ref(true)
const error = ref(null)

// Computed property for filtered comics based on category
const filteredComics = computed(() => {
  const categoryId = route.query.category
  if (!categoryId) return comics.value
  return comics.value.filter(comic => comic.category_id === categoryId)
})

const handleImageError = (event) => {
  event.target.src = '/placeholder-comic.jpg'
}

const fetchData = async () => {
  loading.value = true
  error.value = null
  
  try {
    const response = await api.get('/comics')
    comics.value = response.data
  } catch (err) {
    error.value = err.response?.data?.message || 'Failed to load comics'
    console.error('Error fetching comics:', err)
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  fetchData()
})
</script>

<style scoped>
.line-clamp-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>
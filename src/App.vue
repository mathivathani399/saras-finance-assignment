<template>
  <div class="app-container">
    <header class="header">
      <h1 class="title-glow">Market Explorer</h1>
      <button class="theme-toggle" @click="toggleTheme">
        {{ isDarkMode ? 'Light Mode' : 'Dark Mode' }}
      </button>
    </header>

    <SearchBar @onSearch="performSearch" />

    <Loader v-if="isLoading" />

    <SearchResultList v-else>
      <SearchResultItem
        v-for="result in searchResults"
        :key="result.id"
        :title="result.title"
        :description="result.description"
      />

      <p v-if="hasSearched && searchResults.length === 0" class="no-match-state">
        No results found for your search.
      </p>
    </SearchResultList>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'
import SearchBar from './components/SearchBar.vue'
import SearchResultList from './components/SearchResultList.vue'
import SearchResultItem from './components/SearchResultItem.vue'
import Loader from './components/Loader.vue'

const isLoading = ref(false)
const searchResults = ref([])
const hasSearched = ref(false)
const isDarkMode = ref(false)
let debounceTimer

const fakeDatabase = [
  { id: 1, title: 'Apple Inc', description: 'Tech hardware and software' },
  { id: 2, title: 'Tesla', description: 'Electric vehicles and energy' },
  { id: 3, title: 'Bitcoin', description: 'Digital cryptocurrency' },
  { id: 4, title: 'Ethereum', description: 'Smart contract blockchain' },
  { id: 5, title: 'Nvidia', description: 'GPU and AI technology' },
]

const toggleTheme = () => {
  isDarkMode.value = !isDarkMode.value
}

watch(isDarkMode, (newValue) => {
  if (newValue) {
    document.body.classList.add('dark-theme')
  } else {
    document.body.classList.remove('dark-theme')
  }
})

const performSearch = (query) => {
  clearTimeout(debounceTimer)

  if (query === '') {
    searchResults.value = []
    isLoading.value = false
    hasSearched.value = false
    return
  }

  isLoading.value = true
  hasSearched.value = true

  debounceTimer = setTimeout(() => {
    const lowerQuery = query.toLowerCase()
    searchResults.value = fakeDatabase.filter(
      (item) =>
        item.title.toLowerCase().includes(lowerQuery) ||
        item.description.toLowerCase().includes(lowerQuery),
    )
    isLoading.value = false
  }, 1000)
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap');

body {
  font-family: 'Poppins', sans-serif;
  background: linear-gradient(135deg, #fdfbfb 0%, #ebedee 100%);
  background-attachment: fixed;
  color: #2d3748;
  margin: 0;
  min-height: 100vh;
  transition: background 0.5s ease;
}

/* Adds a soft background animation */
body::before {
  content: '';
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background:
    radial-gradient(circle at 15% 50%, rgba(200, 230, 255, 0.4), transparent 50%),
    radial-gradient(circle at 85% 30%, rgba(255, 230, 240, 0.4), transparent 50%);
  z-index: -1;
}

.app-container {
  max-width: 800px;
  margin: 40px auto;
  padding: 0 20px;
}

.header {
  text-align: center;
  margin-bottom: 40px;
}

.title-glow {
  color: #4a5568;
  font-weight: 600;
  letter-spacing: -0.5px;
}

.theme-toggle {
  background: rgba(255, 255, 255, 0.5);
  backdrop-filter: blur(8px);
  border: 1px solid rgba(255, 255, 255, 0.8);
  color: #4a5568;
  padding: 8px 20px;
  border-radius: 20px;
  cursor: pointer;
  font-size: 0.9rem;
  font-weight: 600;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.02);
  transition: all 0.3s ease;
}

.theme-toggle:hover {
  background: rgba(255, 255, 255, 0.8);
  transform: translateY(-1px);
}

.no-match-state {
  text-align: center;
  color: #a0aec0;
  font-weight: 400;
  margin-top: 2rem;
}

/* --- DARK MODE --- */
body.dark-theme {
  background: linear-gradient(135deg, #0f2027 0%, #203a43 50%, #2c5364 100%);
  color: #e2e8f0;
}

body.dark-theme::before {
  background:
    radial-gradient(circle at 15% 50%, rgba(44, 83, 100, 0.4), transparent 50%),
    radial-gradient(circle at 85% 30%, rgba(15, 32, 39, 0.4), transparent 50%);
}

body.dark-theme .title-glow {
  color: #ffffff;
}

body.dark-theme .theme-toggle {
  background: rgba(0, 0, 0, 0.3);
  color: #e2e8f0;
  border-color: rgba(255, 255, 255, 0.1);
}

body.dark-theme .theme-toggle:hover {
  background: rgba(0, 0, 0, 0.5);
}

body.dark-theme .search-box {
  background: rgba(0, 0, 0, 0.2) !important;
  color: #ffffff !important;
  border-color: rgba(255, 255, 255, 0.1) !important;
}

body.dark-theme .search-box::placeholder {
  color: rgba(255, 255, 255, 0.5);
}

body.dark-theme .result-card {
  background: rgba(0, 0, 0, 0.2) !important;
  border-color: rgba(255, 255, 255, 0.05) !important;
}

body.dark-theme .result-title {
  color: #ffffff !important;
}

body.dark-theme .result-desc {
  color: #cbd5e0 !important;
  border-top-color: rgba(255, 255, 255, 0.1) !important;
}
</style>

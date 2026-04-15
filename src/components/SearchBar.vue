<template>
  <div class="search-wrapper">
    <input
      type="text"
      class="search-box"
      placeholder="Search here..."
      v-model="inputValue"
      @input="$emit('onSearch', inputValue)"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue'

const inputValue = ref('')
defineEmits(['onSearch'])
</script>

<style scoped>
.search-wrapper {
  display: flex;
  justify-content: center;
  margin: 2rem 0 3rem 0;
}

.search-box {
  width: 100%;
  max-width: 600px;
  padding: 16px 24px;
  font-size: 1.1rem;
  background: rgba(255, 255, 255, 0.4);
  backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.6);
  border-radius: 30px;
  box-shadow: 0 8px 32px rgba(31, 38, 135, 0.05);
  transition: all 0.3s ease;
  font-family: inherit;
  color: #2d3748;
}

.search-box::placeholder {
  color: #a0aec0;
}

.search-box:focus {
  background: rgba(255, 255, 255, 0.7);
  border-color: rgba(255, 255, 255, 0.9);
  box-shadow: 0 8px 32px rgba(100, 150, 255, 0.15);
  transform: translateY(-2px);
}
</style>

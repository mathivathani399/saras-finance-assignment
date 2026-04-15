<template>
  <div class="result-card">
    <h3 class="result-title">{{ title }}</h3>

    <p class="result-desc" v-show="isExpanded">
      {{ description }}
    </p>

    <button class="expand-btn" @click="toggleExpand">
      {{ isExpanded ? 'Read Less ▲' : 'Read More ▼' }}
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue'

defineProps({
  title: String,
  description: String,
})

const isExpanded = ref(false)

const toggleExpand = () => {
  isExpanded.value = !isExpanded.value
}
</script>

<style scoped>
.result-card {
  background: rgba(255, 255, 255, 0.45);
  backdrop-filter: blur(16px);
  border-radius: 20px;
  padding: 24px;
  margin-bottom: 20px;
  box-shadow: 0 8px 32px rgba(31, 38, 135, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.5);
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.result-card:hover {
  transform: translateY(-6px) scale(1.01);
  box-shadow: 0 12px 40px rgba(100, 150, 255, 0.1);
  background: rgba(255, 255, 255, 0.65);
}

.result-title {
  margin: 0 0 8px 0;
  color: inherit;
  font-size: 1.3rem;
  font-weight: 600;
}

.result-desc {
  margin: 0 0 12px 0;
  color: inherit;
  opacity: 0.8;
  line-height: 1.6;
  padding-top: 16px;
  border-top: 1px dashed rgba(160, 174, 192, 0.4);
}

.expand-btn {
  background: none;
  border: none;
  color: #667eea;
  font-weight: 600;
  cursor: pointer;
  padding: 0;
  margin-top: 12px;
  font-family: inherit;
  transition: color 0.2s;
  letter-spacing: 0.5px;
}

.expand-btn:hover {
  color: #4c51bf;
}
</style>

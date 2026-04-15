<template>
  <div class="loader-wrapper">
    <div class="spinner"></div>
  </div>
</template>

<script setup></script>

<style scoped>
.loader-wrapper {
  display: flex;
  justify-content: center;
  margin: 3rem 0;
}

.spinner {
  width: 48px;
  height: 48px;
  border: 4px solid rgba(255, 255, 255, 0.3);
  border-top: 4px solid #667eea;
  border-radius: 50%;
  animation: spin 1s cubic-bezier(0.5, 0.1, 0.4, 0.9) infinite;
  box-shadow: 0 0 15px rgba(100, 150, 255, 0.2);
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>

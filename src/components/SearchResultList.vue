<template>
  <div class="results-list">
    <slot>
      <p class="empty-state">Start typing to search...</p>
    </slot>
  </div>
</template>

<script setup></script>

<style scoped>
.results-list {
  max-width: 600px;
  margin: 0 auto;
  padding: 10px;
}

.empty-state {
  text-align: center;
  color: #8c8c8c;
  font-style: italic;
  margin-top: 2rem;
}
</style>

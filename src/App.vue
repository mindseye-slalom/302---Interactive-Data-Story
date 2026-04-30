<template>
  <div id="app" class="app">
    <!-- Scroll Progress Bar -->
    <ScrollProgress />
    
    <!-- Main Story Container -->
    <main class="story-container">
      <QualityStory />
    </main>
  </div>
</template>

<script setup lang="ts">
import ScrollProgress from './components/ScrollProgress.vue'
import QualityStory from './views/QualityStory.vue'
</script>

<style scoped>
.app {
  width: 100%;
  min-height: 100vh;
  background: linear-gradient(135deg, #0d1b2a 0%, #1b263b 100%);
}

.story-container {
  width: 100%;
  max-width: 1400px;
  margin: 0 auto;
}
</style>

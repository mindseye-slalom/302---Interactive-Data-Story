<template>
  <div id="app" class="app">
    <!-- Skip to main content link for keyboard navigation -->
    <a href="#main-story" class="skip-link">Skip to Main Content</a>
    
    <!-- Scroll Progress Bar -->
    <ScrollProgress />
    
    <!-- Main Story Container -->
    <main id="main-story" class="story-container">
      <QualityStory />
    </main>
  </div>
</template>

<script setup lang="ts">
import ScrollProgress from './components/ScrollProgress.vue'
import QualityStory from './views/QualityStory.vue'
</script>

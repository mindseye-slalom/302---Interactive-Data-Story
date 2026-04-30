<template>
  <div 
    class="scroll-progress" 
    :style="{ width: scrollProgress + '%' }"
    role="progressbar"
    :aria-valuenow="Math.round(scrollProgress)"
    aria-valuemin="0"
    aria-valuemax="100"
    aria-label="Page scroll progress"
  ></div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const scrollProgress = ref(0)

const handleScroll = () => {
  const scrollTop = window.scrollY || document.documentElement.scrollTop
  const docHeight = document.documentElement.scrollHeight - window.innerHeight
  const scrollPercent = docHeight > 0 ? (scrollTop / docHeight) * 100 : 0
  scrollProgress.value = scrollPercent
  // Use scaleX for performant width animation
  const element = document.querySelector('.scroll-progress') as HTMLElement
  if (element) {
    element.style.setProperty('--progress-scale', (scrollPercent / 100).toString())
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.scroll-progress {
  position: fixed;
  top: 0;
  left: 0;
  height: 4px;
  background: linear-gradient(90deg, var(--color-cyan) 0%, var(--color-bright-blue) 100%);
  width: 0%;
  transition: transform 100ms linear;
  transform-origin: left;
  z-index: 1000;
  box-shadow: 0 0 20px rgba(0, 217, 255, 0.5);
}
</style>

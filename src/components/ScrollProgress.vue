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

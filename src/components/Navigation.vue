<template>
  <nav class="flex items-center space-x-2 sm:space-x-4">
    <RouterLink
      to="/"
      class="text-gray-600 hover:text-gray-900 px-2 sm:px-3 py-2 rounded-md text-sm font-medium transition-colors border border-transparent hover:border-gray-300"
      active-class="text-blue-600 bg-blue-50 border-blue-200"
    >
      Users
    </RouterLink>
    <RouterLink
      to="/about"
      class="text-gray-600 hover:text-gray-900 px-2 sm:px-3 py-2 rounded-md text-sm font-medium transition-colors border border-transparent hover:border-gray-300"
      active-class="text-blue-600 bg-blue-50 border-blue-200"
    >
      About
    </RouterLink>
  </nav>
</template>

<script setup lang="ts">
import { RouterLink } from 'vue-router'
</script>

<style scoped>
/* Enhanced hover effects for navigation */
nav a {
  position: relative;
  overflow: hidden;
}

nav a::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transition: left 0.5s;
}

nav a:hover::before {
  left: 100%;
}
</style> 
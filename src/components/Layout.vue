<template>
  <div class="min-h-screen bg-gray-100 w-screen overflow-x-hidden">
    <!-- Header Section with Navigation -->
    <div class="w-full bg-gray-100 py-4 sm:py-6">
      <div class="w-full px-4 sm:px-6 lg:px-8 xl:px-12 2xl:px-16">
        <div class="flex flex-col sm:flex-row sm:items-start sm:justify-between gap-4">
          <!-- Left side: Title and Description -->
          <div class="flex-1">
            <img src="@/assets/kiratech_logo.png" alt="App Logo" class="h-12 w-auto sm:h-16" />
          </div>
          
          <!-- Right side: Navigation -->
          <div class="flex-shrink-0 sm:ml-6">
            <Navigation />
          </div>
        </div>
      </div>
    </div>

    <!-- Content Slot -->
    <slot />
  </div>
</template>

<script setup lang="ts">
import Navigation from './Navigation.vue'
</script>

<style scoped>
/* Ensure full viewport width */
div {
  box-sizing: border-box;
}
</style> 
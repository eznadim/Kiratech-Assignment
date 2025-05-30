<template>
  <div class="min-h-screen w-full flex flex-col">
    <!-- Combined Header + Navigation -->
    <div class="w-full bg-white flex items-center justify-between px-8 py-4 border-b border-gray-200">
      <div class="flex items-center space-x-6">
        <img
          src="@/assets/kiratech_logo.png"
          alt="Kiratech Logo"
          class="h-20 w-25"
        />
        <nav class="flex items-center space-x-2 sm:space-x-4 ml-8">
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
      </div>
      <!-- Right-side icons -->
      <div class="flex items-center space-x-6">
        <button class="text-gray-500 hover:text-gray-700">
          <svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"/>
          </svg>
        </button>
        <button class="text-gray-500 hover:text-gray-700">
          <svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v1m0 14v1m8-8h1M4 12H3m15.364-6.364l.707.707M6.343 17.657l-.707.707m12.728 0l-.707-.707M6.343 6.343l-.707-.707"/>
          </svg>
        </button>
        <button class="text-gray-500 hover:text-gray-700">
          <svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z"/>
          </svg>
        </button>
      </div>
    </div>
    <slot />
  </div>
</template>

<script setup lang="ts">
import { RouterLink } from 'vue-router'
</script>

<style scoped>
/* Ensure full viewport width */
div {
  box-sizing: border-box;
}

.min-h-screen {
  min-height: 100vh;
  width: 100vw;
  max-width: 100vw;
  margin: 0;
  padding: 0;
}
</style> 
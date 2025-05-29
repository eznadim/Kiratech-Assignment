<script setup lang="ts">
import { RouterView } from 'vue-router'
</script>

<template>
  <div id="app" class="min-h-screen bg-white w-full m-0 p-0">
    <main class="w-full m-0 p-0">
      <RouterView />
    </main>
  </div>
</template>

<style>
/* Reset body styles completely */
body {
  background-color: white !important;
  background: white !important;
  display: block !important;
  place-items: unset !important;
  margin: 0 !important;
  padding: 0 !important;
  min-height: 100vh !important;
  color: var(--color-text) !important;
}

/* Also reset html */
html {
  background-color: white !important;
  background: white !important;
}

/* Global styles */
html, body {
  margin: 0;
  padding: 0;
  width: 100%;
}

#app {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  background-color: white;
  width: 100%;
  min-height: 100vh;
  display: block;
}

/* Remove default button styles */
button {
  font-family: inherit;
}

/* Ensure smooth transitions */
* {
  transition-property: color, background-color, border-color, text-decoration-color, fill, stroke;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-duration: 150ms;
}

/* Responsive viewport units fix for mobile */
@supports (height: 100dvh) {
  #app {
    min-height: 100dvh;
  }
}
</style>

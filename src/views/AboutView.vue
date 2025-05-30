<template>
  <Layout
  >
    <!-- Main Content Area -->
    <div class="w-full bg-white">
      <div class="w-full px-4 sm:px-6 lg:px-8 xl:px-12 2xl:px-16 py-8 sm:py-12">
        <!-- Introduction Section -->
        <div class="mb-8 sm:mb-12">
          <div class="prose max-w-none">
            <p class="text-base sm:text-lg lg:text-xl text-gray-600 leading-relaxed">
              This is a Vue3 application that displays a list of users and their details from the 
              <a href="https://randomuser.me/" class="text-blue-600 hover:text-blue-800 underline font-medium" target="_blank" rel="noopener noreferrer">RandomUser.me API</a>.
              Built with modern web technologies for optimal performance and user experience.
            </p>
          </div>
        </div>

        <!-- Features Section -->
        <div class="mb-8 sm:mb-12">
          <h2 class="text-xl sm:text-2xl lg:text-3xl font-bold text-gray-900 mb-6">Features</h2>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6 lg:gap-8">
            <div class="bg-gray-50 rounded-lg p-6 hover:bg-gray-100 transition-colors">
              <div class="flex items-start space-x-4">
                <div class="flex-shrink-0">
                  <svg class="h-6 w-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z"></path>
                  </svg>
                </div>
                <div>
                  <h3 class="text-lg font-semibold text-gray-900 mb-2">Browse Users</h3>
                  <p class="text-gray-600">Browse through a paginated list of 20 random users per page</p>
                </div>
              </div>
            </div>

            <div class="bg-gray-50 rounded-lg p-6 hover:bg-gray-100 transition-colors">
              <div class="flex items-start space-x-4">
                <div class="flex-shrink-0">
                  <svg class="h-6 w-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
                  </svg>
                </div>
                <div>
                  <h3 class="text-lg font-semibold text-gray-900 mb-2">Search & Filter</h3>
                  <p class="text-gray-600">Search users by name, email, or location with real-time filtering</p>
                </div>
              </div>
            </div>

            <div class="bg-gray-50 rounded-lg p-6 hover:bg-gray-100 transition-colors">
              <div class="flex items-start space-x-4">
                <div class="flex-shrink-0">
                  <svg class="h-6 w-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16V4m0 0L3 8m4-4l4 4m6 0v12m0 0l4-4m-4 4l-4-4"></path>
                  </svg>
                </div>
                <div>
                  <h3 class="text-lg font-semibold text-gray-900 mb-2">Sort Options</h3>
                  <p class="text-gray-600">Sort users by name, age, gender, or country in ascending/descending order</p>
                </div>
              </div>
            </div>

            <div class="bg-gray-50 rounded-lg p-6 hover:bg-gray-100 transition-colors">
              <div class="flex items-start space-x-4">
                <div class="flex-shrink-0">
                  <svg class="h-6 w-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path>
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"></path>
                  </svg>
                </div>
                <div>
                  <h3 class="text-lg font-semibold text-gray-900 mb-2">Detailed View</h3>
                  <p class="text-gray-600">View detailed user information in a modal popup with comprehensive data</p>
                </div>
              </div>
            </div>

            <div class="bg-gray-50 rounded-lg p-6 hover:bg-gray-100 transition-colors">
              <div class="flex items-start space-x-4">
                <div class="flex-shrink-0">
                  <svg class="h-6 w-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"></path>
                  </svg>
                </div>
                <div>
                  <h3 class="text-lg font-semibold text-gray-900 mb-2">Pagination</h3>
                  <p class="text-gray-600">Navigate through multiple pages of users with pagination controls</p>
                </div>
              </div>
            </div>

            <div class="bg-gray-50 rounded-lg p-6 hover:bg-gray-100 transition-colors">
              <div class="flex items-start space-x-4">
                <div class="flex-shrink-0">
                  <svg class="h-6 w-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 18h.01M8 21h8a2 2 0 002-2V5a2 2 0 00-2-2H8a2 2 0 00-2 2v14a2 2 0 002 2z"></path>
                  </svg>
                </div>
                <div>
                  <h3 class="text-lg font-semibold text-gray-900 mb-2">Responsive Design</h3>
                  <p class="text-gray-600">Optimized for all devices with mobile-first responsive design</p>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Technology Stack Section -->
        <div class="mb-8 sm:mb-12">
          <h2 class="text-xl sm:text-2xl lg:text-3xl font-bold text-gray-900 mb-6">Technology Stack</h2>
          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 lg:gap-6">
            <div class="bg-gradient-to-br from-green-50 to-green-100 border border-green-200 rounded-lg p-6 text-center hover:shadow-md transition-shadow">
              <div class="text-green-600 text-2xl font-bold mb-2">Vue 3</div>
              <p class="text-green-700 text-sm">Progressive JavaScript framework</p>
            </div>
            
            <div class="bg-gradient-to-br from-blue-50 to-blue-100 border border-blue-200 rounded-lg p-6 text-center hover:shadow-md transition-shadow">
              <div class="text-blue-600 text-2xl font-bold mb-2">TypeScript</div>
              <p class="text-blue-700 text-sm">Type-safe JavaScript</p>
            </div>
            
            <div class="bg-gradient-to-br from-cyan-50 to-cyan-100 border border-cyan-200 rounded-lg p-6 text-center hover:shadow-md transition-shadow">
              <div class="text-cyan-600 text-2xl font-bold mb-2">Tailwind CSS</div>
              <p class="text-cyan-700 text-sm">Utility-first CSS framework</p>
            </div>
            
            <div class="bg-gradient-to-br from-purple-50 to-purple-100 border border-purple-200 rounded-lg p-6 text-center hover:shadow-md transition-shadow">
              <div class="text-purple-600 text-2xl font-bold mb-2">Axios</div>
              <p class="text-purple-700 text-sm">HTTP client for API requests</p>
            </div>
            
            <div class="bg-gradient-to-br from-orange-50 to-orange-100 border border-orange-200 rounded-lg p-6 text-center hover:shadow-md transition-shadow">
              <div class="text-orange-600 text-2xl font-bold mb-2">Vite</div>
              <p class="text-orange-700 text-sm">Fast build tool</p>
            </div>
            
            <div class="bg-gradient-to-br from-pink-50 to-pink-100 border border-pink-200 rounded-lg p-6 text-center hover:shadow-md transition-shadow">
              <div class="text-pink-600 text-2xl font-bold mb-2">Pinia</div>
              <p class="text-pink-700 text-sm">State management</p>
            </div>
          </div>
        </div>

        <!-- API Information Section -->
        <div class="bg-blue-50 border border-blue-200 rounded-lg p-6 lg:p-8">
          <div class="flex items-start space-x-4">
            <div class="flex-shrink-0">
              <svg class="h-8 w-8 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.828 10.172a4 4 0 00-5.656 0l-4 4a4 4 0 105.656 5.656l1.102-1.101m-.758-4.899a4 4 0 005.656 0l4-4a4 4 0 00-5.656-5.656l-1.1 1.1"></path>
              </svg>
            </div>
            <div class="flex-1">
              <h3 class="text-lg sm:text-xl font-bold text-blue-900 mb-3">API Information</h3>
              <p class="text-blue-800 mb-4 leading-relaxed">
                This application uses the <a href="https://randomuser.me/" class="font-semibold underline hover:text-blue-900" target="_blank" rel="noopener noreferrer">RandomUser.me API</a> to fetch user data. 
                The API provides random user data including profile pictures, names, contact information, and location details.
              </p>
              <div class="bg-white rounded-md p-4 border border-blue-200">
                <p class="text-sm text-blue-700 font-mono">
                  GET https://randomuser.me/api/?page=1&results=20
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </Layout>
</template>

<script setup lang="ts">
import Layout from '@/components/Layout.vue'
</script>

<style scoped>
/* Ensure consistent styling */
div {
  box-sizing: border-box;
}
</style>

<template>
  <div
    v-if="isOpen"
    class="fixed inset-0 z-50 overflow-y-auto"
    @click.self="$emit('close')"
  >
    <div class="flex items-center justify-center min-h-screen px-4 pt-4 pb-20 text-center sm:block sm:p-0">
      <!-- Background overlay -->
      <div class="fixed inset-0 transition-opacity bg-gray-500 bg-opacity-75" @click="$emit('close')"></div>

      <!-- Modal content -->
      <div class="inline-block w-full max-w-sm sm:max-w-md lg:max-w-lg p-4 sm:p-6 my-8 overflow-hidden text-left align-middle transition-all transform bg-white shadow-xl rounded-2xl">
        <!-- Header -->
        <div class="flex items-center justify-between mb-4 sm:mb-6">
          <h3 class="text-lg font-medium leading-6 text-gray-900">User Details</h3>
          <button
            @click="$emit('close')"
            class="text-gray-400 hover:text-gray-600 transition-colors p-1"
          >
            <svg class="w-5 h-5 sm:w-6 sm:h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
            </svg>
          </button>
        </div>

        <!-- User information -->
        <div v-if="user" class="space-y-3 sm:space-y-4">
          <!-- Profile picture and basic info -->
          <div class="flex items-center space-x-3 sm:space-x-4 mb-4 sm:mb-6">
            <img
              :src="user.picture.large"
              :alt="`${user.name.first} ${user.name.last}`"
              class="w-16 h-16 sm:w-20 sm:h-20 rounded-full object-cover"
            />
            <div class="flex-1 min-w-0">
              <h4 class="text-lg sm:text-xl font-semibold text-gray-900 truncate">
                {{ user.name.title }} {{ user.name.first }} {{ user.name.last }}
              </h4>
              <p class="text-sm sm:text-base text-gray-600 truncate">{{ user.email }}</p>
              <p class="text-xs sm:text-sm text-gray-500 capitalize">{{ user.gender }}, {{ user.dob.age }} years old</p>
            </div>
          </div>

          <!-- Contact Information -->
          <div class="bg-gray-50 rounded-lg p-3 sm:p-4">
            <h5 class="font-semibold text-gray-900 mb-2 sm:mb-3 text-sm sm:text-base">Contact Information</h5>
            <div class="space-y-1 sm:space-y-2 text-xs sm:text-sm">
              <div class="flex justify-between">
                <span class="text-gray-600">Phone:</span>
                <span class="text-gray-900 text-right">{{ user.phone }}</span>
              </div>
              <div class="flex justify-between">
                <span class="text-gray-600">Cell:</span>
                <span class="text-gray-900 text-right">{{ user.cell }}</span>
              </div>
              <div class="flex justify-between">
                <span class="text-gray-600">Email:</span>
                <span class="text-gray-900 text-right truncate ml-2">{{ user.email }}</span>
              </div>
            </div>
          </div>

          <!-- Location Information -->
          <div class="bg-gray-50 rounded-lg p-3 sm:p-4">
            <h5 class="font-semibold text-gray-900 mb-2 sm:mb-3 text-sm sm:text-base">Location</h5>
            <div class="space-y-1 sm:space-y-2 text-xs sm:text-sm">
              <div class="flex justify-between">
                <span class="text-gray-600">Address:</span>
                <span class="text-gray-900 text-right">
                  {{ user.location.street.number }} {{ user.location.street.name }}
                </span>
              </div>
              <div class="flex justify-between">
                <span class="text-gray-600">City:</span>
                <span class="text-gray-900">{{ user.location.city }}</span>
              </div>
              <div class="flex justify-between">
                <span class="text-gray-600">State:</span>
                <span class="text-gray-900">{{ user.location.state }}</span>
              </div>
              <div class="flex justify-between">
                <span class="text-gray-600">Country:</span>
                <span class="text-gray-900">{{ user.location.country }}</span>
              </div>
              <div class="flex justify-between">
                <span class="text-gray-600">Postcode:</span>
                <span class="text-gray-900">{{ user.location.postcode }}</span>
              </div>
            </div>
          </div>

          <!-- Additional Information -->
          <div class="bg-gray-50 rounded-lg p-3 sm:p-4">
            <h5 class="font-semibold text-gray-900 mb-2 sm:mb-3 text-sm sm:text-base">Additional Information</h5>
            <div class="space-y-1 sm:space-y-2 text-xs sm:text-sm">
              <div class="flex justify-between">
                <span class="text-gray-600">Username:</span>
                <span class="text-gray-900">{{ user.login.username }}</span>
              </div>
              <div class="flex justify-between">
                <span class="text-gray-600">Date of Birth:</span>
                <span class="text-gray-900 text-right">{{ formatDate(user.dob.date) }}</span>
              </div>
              <div class="flex justify-between">
                <span class="text-gray-600">Registered:</span>
                <span class="text-gray-900 text-right">{{ formatDate(user.registered.date) }}</span>
              </div>
              <div class="flex justify-between">
                <span class="text-gray-600">Nationality:</span>
                <span class="text-gray-900">{{ user.nat }}</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Close button -->
        <div class="mt-4 sm:mt-6 flex justify-end">
          <button
            @click="$emit('close')"
            class="px-3 sm:px-4 py-2 text-xs sm:text-sm font-medium text-white bg-blue-600 border border-transparent rounded-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 transition-colors"
          >
            Close
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { User } from '@/services/userService';

defineProps<{
  isOpen: boolean;
  user: User | null;
}>();

defineEmits<{
  close: [];
}>();

const formatDate = (dateString: string) => {
  return new Date(dateString).toLocaleDateString('en-US', {
    year: 'numeric',
    month: 'long',
    day: 'numeric',
  });
};
</script> 
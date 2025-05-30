<template>
  <div
    class="w-full border-b border-gray-200 hover:bg-gray-50 transition-colors duration-200 cursor-pointer bg-white"
    @click="$emit('selectUser', user)"
  >
    <div class="w-full px-4 sm:px-6 lg:px-8 xl:px-12 2xl:px-16 py-4 sm:py-5">
      <div class="flex items-center justify-between w-full">
        <!-- Left side: Profile image and main info -->
        <div class="flex items-center space-x-3 sm:space-x-4 lg:space-x-6 flex-1 min-w-0">
          <img
            :src="user.picture.medium"
            :alt="`${user.name.first} ${user.name.last}`"
            class="w-12 h-12 sm:w-14 sm:h-14 lg:w-16 lg:h-16 xl:w-18 xl:h-18 rounded-full object-cover flex-shrink-0"
          />
          
          <div class="flex-1 min-w-0">
            <h3 class="text-base sm:text-lg lg:text-xl xl:text-2xl font-semibold text-gray-900 truncate">
              {{ user.name.title }} {{ user.name.first }} {{ user.name.last }}
            </h3>
            <p class="text-sm sm:text-base lg:text-lg text-gray-600 truncate">{{ user.email }}</p>
            <p class="text-xs sm:text-sm lg:text-base text-gray-500 truncate">
              {{ user.location.city }}, {{ user.location.country }}
            </p>
          </div>
        </div>
        
        <!-- Right side: Data values only (table-like columns) -->
        <div class="flex items-center space-x-6 sm:space-x-8 lg:space-x-12 xl:space-x-16 flex-shrink-0">
          <!-- Date -->
          <div class="text-center min-w-[100px] lg:min-w-[120px] hidden md:block">
            <p class="text-sm lg:text-base font-medium text-gray-900">{{ formatDate(user.registered.date) }}</p>
          </div>
          
          <!-- Gender -->
          <div class="text-center min-w-[60px] lg:min-w-[80px] hidden sm:block">
            <p class="text-sm lg:text-base font-medium text-gray-900 capitalize">{{ user.gender }}</p>
          </div>
          
          <!-- Country -->
          <div class="text-center min-w-[80px] lg:min-w-[100px] xl:min-w-[120px] hidden lg:block">
            <p class="text-sm lg:text-base font-medium text-gray-900 truncate">{{ user.location.country }}</p>
          </div>
          
          <!-- Email (shown only on larger screens) -->
          <div class="text-center min-w-[120px] lg:min-w-[140px] xl:min-w-[160px] hidden xl:block">
            <p class="text-sm lg:text-base font-medium text-gray-900 truncate">{{ user.email }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { User } from '@/services/userService';

defineProps<{
  user: User;
}>();

defineEmits<{
  selectUser: [user: User];
}>();

const formatDate = (dateString: string) => {
  const date = new Date(dateString);
  return date.toLocaleDateString('en-GB', {
    day: '2-digit',
    month: 'short',
    year: 'numeric'
  });
};
</script> 
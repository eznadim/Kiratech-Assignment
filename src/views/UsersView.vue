<template>
  <Layout>
    <!-- Blue Banner Section - Modified -->
    <div class="w-full bg-cyan-400 pt-8 relative overflow-visible">
      <div class="px-4 sm:px-6 lg:px-8 xl:px-12 2xl:px-16 flex flex-col sm:flex-row sm:items-end sm:space-x-8 relative">
        <img
           src="@/assets/Avatar.png"
          alt="John Doe"
          class="w-60 h-60 object-cover z-20 -mb-16"
        />
        <div class="flex flex-col items-center sm:items-start mt-4 sm:mt-0 sm:ml-4 pb-8"> 
          <h1 class="text-white text-3xl font-bold mb-2">John Doe</h1>
          <p class="text-white text-opacity-80 mb-4">Last online: 2 days ago</p>
          <div class="flex space-x-4">
            <button class="flex items-center px-5 py-2 bg-white text-cyan-500 font-semibold rounded-md shadow hover:bg-gray-100 transition">
              <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3"/>
              </svg>
              Send Message
            </button>
            <button class="flex items-center px-5 py-2 border-2 border-white text-white font-semibold rounded-md hover:bg-white hover:text-cyan-500 transition">
              <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/>
              </svg>
              Add Friend
            </button>
          </div>
        </div>
      </div>
    </div>

    <div class="w-full bg-white border-b border-gray-200 pt-20 pb-6">
      <div class="w-full px-4 sm:px-6 lg:px-8 xl:px-12 2xl:px-16">
        <div class="flex flex-col xl:flex-row xl:items-center xl:justify-between gap-4">
          <div class="relative flex-1 w-full sm:max-w-md lg:max-w-lg xl:max-w-xl">
            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none z-10">
              <svg class="h-4 w-4 sm:h-5 sm:w-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
              </svg>
            </div>
            <input
              v-model="searchQuery"
              type="text"
              placeholder="Search users by name, email, or location..."
              class="block w-full pl-8 sm:pl-10 pr-3 py-2 text-sm sm:text-base border border-gray-300 rounded-md leading-5 bg-white text-gray-900 placeholder-gray-500 focus:outline-none focus:placeholder-gray-400 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 shadow-sm"
            />
          </div>

          <div class="flex flex-col sm:flex-row gap-3 sm:gap-4">
            <div class="relative z-20">
              <select
                v-model="sortCriteria"
                class="block w-full sm:w-auto px-3 py-2 text-sm border border-gray-300 rounded-md bg-white text-gray-900 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 appearance-none pr-8 shadow-sm cursor-pointer"
                style="background-color: white; color: #111827;"
              >
                <option value="" style="background-color: white; color: #111827;">Sort by...</option>
                <option value="date" style="background-color: white; color: #111827;">Date (Newest First)</option>
                <option value="date-desc" style="background-color: white; color: #111827;">Date (Oldest First)</option>
                <option value="name" style="background-color: white; color: #111827;">Name (A-Z)</option>
                <option value="name-desc" style="background-color: white; color: #111827;">Name (Z-A)</option>
                <option value="age" style="background-color: white; color: #111827;">Age (Low-High)</option>
                <option value="age-desc" style="background-color: white; color: #111827;">Age (High-Low)</option>
                <option value="gender" style="background-color: white; color: #111827;">Gender</option>
                <option value="country" style="background-color: white; color: #111827;">Country</option>
              </select>
              <div class="absolute inset-y-0 right-0 flex items-center pr-2 pointer-events-none z-10">
                <svg class="h-4 w-4 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
                </svg>
              </div>
            </div>

            <button
              @click="refreshUsers"
              :disabled="loading"
              class="inline-flex items-center justify-center px-3 sm:px-4 py-2 border border-transparent rounded-md shadow-sm text-xs sm:text-sm font-medium text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 disabled:opacity-50 disabled:cursor-not-allowed transition-colors w-full sm:w-auto sm:min-w-[120px]"
            >
              <svg
                class="w-3 h-3 sm:w-4 sm:h-4 mr-2"
                :class="{ 'animate-spin': loading }"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"></path>
              </svg>
              {{ loading ? 'Loading...' : 'Refresh' }}
            </button>
          </div>
        </div>

        <div class="mt-4 flex flex-col sm:flex-row sm:items-center sm:justify-between gap-2">
          <div class="text-xs sm:text-sm text-gray-600">
            Showing {{ sortedAndFilteredUsers.length }} of {{ users.length }} users (Page {{ currentPage }})
            <span v-if="sortCriteria" class="text-blue-600">
              • Sorted by {{ getSortLabel(sortCriteria) }}
            </span>
          </div>
          <div class="text-xs sm:text-sm text-gray-500">
            {{ users.length }} users loaded per page
          </div>
        </div>
      </div>
    </div>

    <div class="w-full bg-white">
      <div class="w-full px-4 sm:px-6 lg:px-8 xl:px-12 2xl:px-16">
        <div v-if="loading && users.length === 0" class="flex justify-center items-center py-12">
          <div class="text-center">
            <svg class="animate-spin h-6 w-6 sm:h-8 sm:w-8 text-blue-600 mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"></path>
            </svg>
            <p class="text-sm sm:text-base text-gray-500">Loading users...</p>
          </div>
        </div>

        <div v-else-if="error" class="text-center py-12">
          <div class="text-red-600 mb-4">
            <svg class="h-10 w-10 sm:h-12 sm:w-12 mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-2.5L13.732 4c-.77-.833-1.964-.833-2.732 0L4.082 16.5c-.77.833.192 2.5 1.732 2.5z"></path>
            </svg>
          </div>
          <h3 class="text-base sm:text-lg font-medium text-gray-900 mb-2">Failed to load users</h3>
          <p class="text-sm sm:text-base text-gray-500 mb-4">{{ error }}</p>
          <button
            @click="() => fetchUsers()"
            class="inline-flex items-center px-3 sm:px-4 py-2 border border-transparent rounded-md shadow-sm text-xs sm:text-sm font-medium text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
          >
            Try Again
          </button>
        </div>

        <div v-else-if="sortedAndFilteredUsers.length > 0" class="w-full">
          <!-- Table Structure -->
          <div class="overflow-x-auto">
            <table class="w-full border-collapse">
              <!-- Table Header -->
              <thead>
                <tr class="bg-gray-50 border-b border-gray-300">
                  <th class="px-4 sm:px-6 lg:px-8 py-3 text-left text-sm font-semibold text-gray-600 uppercase tracking-wide">Name</th>
                  <th class="px-4 py-3 text-center text-sm font-semibold text-gray-600 uppercase tracking-wide hidden md:table-cell">Date</th>
                  <th class="px-4 py-3 text-center text-sm font-semibold text-gray-600 uppercase tracking-wide hidden sm:table-cell">Gender</th>
                  <th class="px-4 py-3 text-center text-sm font-semibold text-gray-600 uppercase tracking-wide hidden lg:table-cell">Country</th>
                  <th class="px-4 py-3 text-center text-sm font-semibold text-gray-600 uppercase tracking-wide hidden xl:table-cell">Email</th>
                </tr>
              </thead>
              <!-- Table Body -->
              <tbody>
                <tr 
                  v-for="user in sortedAndFilteredUsers" 
                  :key="user.login.uuid"
                  class="border-b border-gray-200 hover:bg-gray-50 transition-colors duration-200 cursor-pointer"
                  @click="selectUser(user)"
                >
                  <!-- Name Column -->
                  <td class="px-4 sm:px-6 lg:px-8 py-4 sm:py-5">
                    <div class="flex items-center space-x-3 sm:space-x-4">
                      <img
                        :src="user.picture.medium"
                        :alt="`${user.name.first} ${user.name.last}`"
                        class="w-12 h-12 sm:w-14 sm:h-14 lg:w-16 lg:h-16 rounded-full object-cover flex-shrink-0"
                      />
                      <div class="min-w-0">
                        <h3 class="text-base sm:text-lg font-semibold text-gray-900 truncate">
                          {{ user.name.title }} {{ user.name.first }} {{ user.name.last }}
                        </h3>
                        <p class="text-sm text-gray-600 truncate">{{ user.email }}</p>
                        <p class="text-xs text-gray-500 truncate">
                          {{ user.location.city }}, {{ user.location.country }}
                        </p>
                      </div>
                    </div>
                  </td>
                  
                  <!-- Date Column -->
                  <td class="px-4 py-4 text-center text-sm font-medium text-gray-900 hidden md:table-cell">
                    {{ formatDate(user.registered.date) }}
                  </td>
                  
                  <!-- Gender Column -->
                  <td class="px-4 py-4 text-center text-sm font-medium text-gray-900 capitalize hidden sm:table-cell">
                    {{ user.gender }}
                  </td>
                  
                  <!-- Country Column -->
                  <td class="px-4 py-4 text-center text-sm font-medium text-gray-900 hidden lg:table-cell">
                    {{ user.location.country }}
                  </td>
                  
                  <!-- Email Column -->
                  <td class="px-4 py-4 text-center text-sm font-medium text-gray-900 truncate hidden xl:table-cell">
                    {{ user.email }}
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>

        <div v-else-if="searchQuery && sortedAndFilteredUsers.length === 0" class="text-center py-12">
          <div class="text-gray-400 mb-4">
            <svg class="h-10 w-10 sm:h-12 sm:w-12 mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
            </svg>
          </div>
          <h3 class="text-base sm:text-lg font-medium text-gray-900 mb-2">No users found</h3>
          <p class="text-sm sm:text-base text-gray-500">Try adjusting your search criteria</p>
        </div>
      </div>
    </div>

    <div class="w-full bg-white border-t border-gray-200 py-4">
      <div class="w-full px-4 sm:px-6 lg:px-8 xl:px-12 2xl:px-16">
        <div class="flex flex-col lg:flex-row lg:items-center lg:justify-between gap-4">
          <div class="text-sm text-gray-700 text-center lg:text-left">
            Page <span class="font-medium">{{ currentPage }}</span> 
            <span class="hidden sm:inline">of users from RandomUser API</span>
          </div>

          <div class="flex items-center justify-center space-x-1">
            <button
              @click="goToPage(currentPage - 1)"
              :disabled="currentPage <= 1 || loading"
              class="relative inline-flex items-center px-2 py-2 rounded-l-md border border-gray-300 bg-white text-sm font-medium text-gray-500 hover:bg-gray-50 focus:z-10 focus:outline-none focus:ring-1 focus:ring-blue-500 focus:border-blue-500 disabled:opacity-50 disabled:cursor-not-allowed transition-colors"
            >
              <span class="sr-only">Previous</span>
              <svg class="h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
              </svg>
            </button>

            <template v-for="page in visiblePages" :key="page">
              <button
                v-if="page !== '...'"
                @click="goToPage(page as number)"
                :disabled="loading"
                :class="[
                  'relative inline-flex items-center px-3 py-2 border text-sm font-medium focus:z-10 focus:outline-none focus:ring-1 focus:ring-blue-500 focus:border-blue-500 transition-colors',
                  currentPage === page
                    ? 'z-10 bg-blue-50 border-blue-500 text-blue-600'
                    : 'bg-white border-gray-300 text-gray-500 hover:bg-gray-50'
                ]"
              >
                {{ page }}
              </button>
              <span
                v-else
                class="relative inline-flex items-center px-3 py-2 border border-gray-300 bg-white text-sm font-medium text-gray-700"
              >
                ...
              </span>
            </template>

            <button
              @click="goToPage(currentPage + 1)"
              :disabled="loading"
              class="relative inline-flex items-center px-2 py-2 rounded-r-md border border-gray-300 bg-white text-sm font-medium text-gray-500 hover:bg-gray-50 focus:z-10 focus:outline-none focus:ring-1 focus:ring-blue-500 focus:border-blue-500 disabled:opacity-50 disabled:cursor-not-allowed transition-colors"
            >
              <span class="sr-only">Next</span>
              <svg class="h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
              </svg>
            </button>

            <div class="hidden lg:flex items-center ml-4 space-x-2">
              <span class="text-sm text-gray-500">Go to:</span>
              <input
                v-model.number="jumpToPageInput"
                @keyup.enter="jumpToPage"
                type="number"
                min="1"
                placeholder="Page"
                class="w-16 px-2 py-1 text-sm border border-gray-300 rounded-md bg-white text-gray-900 focus:outline-none focus:ring-1 focus:ring-blue-500 focus:border-blue-500"
              />
              <button
                @click="jumpToPage"
                :disabled="loading || !jumpToPageInput"
                class="inline-flex items-center px-2 py-1 border border-transparent text-sm font-medium rounded-md text-blue-600 bg-blue-100 hover:bg-blue-200 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 disabled:opacity-50 disabled:cursor-not-allowed transition-colors"
              >
                Go
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <UserModal
      :is-open="modalOpen"
      :user="selectedUser"
      @close="closeModal"
    />
  </Layout>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue';
import { userService, type User } from '@/services/userService';
import UserCard from '@/components/UserCard.vue';
import UserModal from '@/components/UserModal.vue';
import Layout from '@/components/Layout.vue';

const users = ref<User[]>([]);
const loading = ref(false);
const error = ref<string | null>(null);
const searchQuery = ref('');
const sortCriteria = ref('');
const modalOpen = ref(false);
const selectedUser = ref<User | null>(null);

// Pagination state
const currentPage = ref(1);
const jumpToPageInput = ref<number | null>(null);

// Computed property for filtered users based on search query
const filteredUsers = computed(() => {
  if (!searchQuery.value.trim()) {
    return users.value;
  }

  const query = searchQuery.value.toLowerCase().trim();
  return users.value.filter(user => {
    const fullName = `${user.name.first} ${user.name.last}`.toLowerCase();
    const email = user.email.toLowerCase();
    const location = `${user.location.city} ${user.location.country}`.toLowerCase();
    
    return fullName.includes(query) || 
           email.includes(query) || 
           location.includes(query);
  });
});

// Computed property for sorted and filtered users
const sortedAndFilteredUsers = computed(() => {
  const filtered = filteredUsers.value;
  
  if (!sortCriteria.value) {
    return filtered;
  }

  const sorted = [...filtered].sort((a, b) => {
    switch (sortCriteria.value) {
      case 'date':
        return new Date(b.registered.date).getTime() - new Date(a.registered.date).getTime();
      case 'date-desc':
        return new Date(a.registered.date).getTime() - new Date(b.registered.date).getTime();
      case 'name':
        return `${a.name.first} ${a.name.last}`.localeCompare(`${b.name.first} ${b.name.last}`);
      case 'name-desc':
        return `${b.name.first} ${b.name.last}`.localeCompare(`${a.name.first} ${a.name.last}`);
      case 'age':
        return a.dob.age - b.dob.age;
      case 'age-desc':
        return b.dob.age - a.dob.age;
      case 'gender':
        return a.gender.localeCompare(b.gender);
      case 'country':
        return a.location.country.localeCompare(b.location.country);
      default:
        return 0;
    }
  });

  return sorted;
});

// Computed property for visible page numbers
const visiblePages = computed(() => {
  const pages: (number | string)[] = [];
  const maxVisiblePages = 5;
  const current = currentPage.value;
  
  // Always show first page
  pages.push(1);
  
  if (current > 4) {
    pages.push('...');
  }
  
  // Show pages around current page
  const start = Math.max(2, current - 1);
  const end = Math.min(current + 1, Math.max(2, current + 1));
  
  for (let i = start; i <= end; i++) {
    if (i !== 1 && !pages.includes(i)) {
      pages.push(i);
    }
  }
  
  // Show current page if not already included
  if (!pages.includes(current) && current !== 1) {
    pages.push(current);
  }
  
  return pages.sort((a, b) => {
    if (typeof a === 'string') return 1;
    if (typeof b === 'string') return -1;
    return a - b;
  });
});

// Get sort label for display
const getSortLabel = (criteria: string) => {
  const labels: Record<string, string> = {
    'date': 'Date (Newest First)',
    'date-desc': 'Date (Oldest First)',
    'name': 'Name (A-Z)',
    'name-desc': 'Name (Z-A)',
    'age': 'Age (Low-High)',
    'age-desc': 'Age (High-Low)',
    'gender': 'Gender',
    'country': 'Country'
  };
  return labels[criteria] || criteria;
};

// Format date function
const formatDate = (dateString: string) => {
  const date = new Date(dateString);
  return date.toLocaleDateString('en-GB', {
    day: '2-digit',
    month: 'short',
    year: 'numeric'
  });
};

// Fetch users from API with pagination
const fetchUsers = async (page: number = currentPage.value) => {
  try {
    loading.value = true;
    error.value = null;
    const response = await userService.getUsersPaginated(page, 20);
    users.value = response.results;
    currentPage.value = page;
  } catch (err) {
    error.value = 'Failed to fetch users. Please check your internet connection and try again.';
    console.error('Error fetching users:', err);
  } finally {
    loading.value = false;
  }
};

// Go to specific page
const goToPage = (page: number) => {
  if (page >= 1 && page !== currentPage.value && !loading.value) {
    fetchUsers(page);
  }
};

// Jump to page from input
const jumpToPage = () => {
  if (jumpToPageInput.value && jumpToPageInput.value >= 1) {
    goToPage(jumpToPageInput.value);
    jumpToPageInput.value = null;
  }
};

// Refresh users (re-fetch current page)
const refreshUsers = () => {
  fetchUsers(currentPage.value);
};

// Select a user to show in modal
const selectUser = (user: User) => {
  selectedUser.value = user;
  modalOpen.value = true;
};

// Close modal
const closeModal = () => {
  modalOpen.value = false;
  selectedUser.value = null;
};

// Load users on component mount
onMounted(() => {
  fetchUsers(1);
});
</script>

<style scoped>
/* Ensure this component uses full viewport width */
div {
  box-sizing: border-box;
}

/* Force full viewport width for the main container */
.min-h-screen {
  width: 100vw;
  max-width: 100vw;
  margin: 0;
  padding: 0;
}

/* Ensure no overflow issues */
:deep(body) {
  margin: 0;
  padding: 0;
  overflow-x: hidden;
}

/* Responsive scaling for larger screens */
@media (min-width: 1920px) {
  .text-2xl { font-size: 2rem; }
  .text-3xl { font-size: 2.5rem; }
  .text-4xl { font-size: 3rem; }
  .text-5xl { font-size: 3.5rem; }
}

/* Ensure profile images render correctly at larger sizes */
.xl\:w-18 {
  width: 4.5rem;
}
.xl\:h-18 {
  height: 4.5rem;
}
</style>

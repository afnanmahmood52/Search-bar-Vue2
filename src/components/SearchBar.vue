<template>
  <div class="relative flex items-center">
    <input
      v-model="searchQuery"
      @input="debouncedSearch"
      type="text"
      :class="[
        'appearance-none bg-transparent rounded-lg w-full text-gray-700 py-4 pl-12 pr-4 leading-tight focus:outline-none',
        api_call_status === 'error' ? 'border-2 border-red-700' : 'border-2 border-gray-300',
        'focus:border-blue-700 border-2'  // Add this for focus styling
      ]"
      placeholder="Search..."
    />
    <div class="absolute top-3 transform w-6 h-6 text-black" style="left: 13px;">
      <svg fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 10-14 0 7 7 0 0014 0z"></path>
      </svg>
    </div>
  </div>
</template>

<script>
import { debounce } from '../utils/debounce';

export default {
  props: {
    api_call_status: {
      type: String,
      required: true
    },
    searchQuery: {
      type: String,
      required: true
    }
  },
  methods: {
    onSearch() {
      this.$emit('search', this.searchQuery);
      this.$emit('reset-tags'); // Emit event to reset tags
    },
    debouncedSearch: debounce(function() {
      this.onSearch();
    }, 300),
  },
};
</script>

<style scoped>
/* No additional styling needed */
</style>

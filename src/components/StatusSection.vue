<template>
  <div class="flex flex-col text-gray-700">
    <!-- Other content above -->
    <div :class="statusClass" class="mt-auto text-left text-sm">
      {{ status_message }}
    </div>
  </div>
</template>

<script>
import { API_STATUSES } from '../constants/constants';

export default {
  props: {
    status_message: {
      type: String,
      required: true,
    },
    api_call_status: {
      type: String,
      required: true,
    },
  },
  computed: {
    statusClass() {
      // Adjust this logic based on how you identify error messages
      if (this.api_call_status === API_STATUSES.ERROR) {
        return 'text-red-600'; // Tailwind class for red text
      }
      return 'text-gray-700'; // Default text color
    },
  },
};
</script>

<style scoped>
/* Add any additional styling if needed */
</style>

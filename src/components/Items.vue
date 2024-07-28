<template>
  <div>
    <!-- Loader spinner -->
    <div v-if="apiCallStatus === API_STATUSES.LOADING" class="flex justify-center items-center h-full py-10">
      <img :src="loaderSvg" alt="Loading" class="spinner"/>
    </div>

    <!-- Empty data -->
    <div v-if="apiCallStatus === API_STATUSES.EMPTY_DATA" class="flex justify-center items-center h-full py-10">
      <img :src="emptyDataSvg" alt="No Data" />
    </div>

    <!-- Error -->
    <div v-if="apiCallStatus === API_STATUSES.ERROR" class="flex justify-center items-center h-full py-10">
      <img :src="errorSvg" alt="Error" />
    </div>

     <!-- Success (display items) -->
    <div
      v-if="apiCallStatus === API_STATUSES.SUCCESS"
      class="py-3 h-64 overflow-y-auto custom-scrollbar"
    >
      <CardItem v-for="item in items" :key="item.id" :item="item" />
    </div>
  </div>
</template>

<script>
import CardItem from './CardItem.vue';
import { API_STATUSES } from '../constants/constants';
import loaderSvg from '@/assets/icons/loader.svg';
import emptyDataSvg from '@/assets/icons/searching_results.svg';
import errorSvg from '@/assets/icons/error_image.svg';

export default {
  components: {
    CardItem,
  },
  props: {
    items: {
      type: Array,
      required: true,
    },
    apiCallStatus: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      API_STATUSES,
      loaderSvg,
      emptyDataSvg,
      errorSvg,
    };
  },
};
</script>

<style scoped>
/* Add any additional styling here */
@keyframes rotate {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.spinner {
  animation: rotate 1s linear infinite;
}

/* Custom scrollbar styles */
.custom-scrollbar::-webkit-scrollbar {
  width: 4px; /* Width of the scrollbar */
}

.custom-scrollbar::-webkit-scrollbar-track {
  background: transparent; /* Background of the scrollbar track */
}

.custom-scrollbar::-webkit-scrollbar-thumb {
  background: lightgray; /* Color of the scrollbar thumb */
}

.custom-scrollbar::-webkit-scrollbar-thumb:hover {
  background: lightgray; /* Color of the scrollbar thumb on hover */
}
</style>

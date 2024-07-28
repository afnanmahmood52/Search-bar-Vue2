<template>
  <div class="flex items-center py-2 card-bag-color group rounded-lg">
    <!-- Image div taking 20% width -->
    <div class="flex-shrink-0 w-1/5 h-20 rounded-lg overflow-hidden flex items-center justify-center  ml-2">
      <div class="h-20 w-20 bg-white p-3">
        <img :src="item.image" alt="item image" class="object-cover w-full h-full" />
      </div>
    </div>

    <!-- Content div taking 80% width -->
    <div class="flex-grow pl-2 truncate w-3/5">
      <h2 class="font-bold text-left">{{ item.title }}</h2>
      <p class="text-gray-600 text-left truncate">{{ item.description }}</p>
    </div>

    <!-- The div to show/hide on hover, taking 20% width -->
    <div class="flex-shrink-0 w-1/5 h-14 rounded-lg overflow-hidden flex justify-end items-center p-3 up-arrow-div">
      <img :src="upArrow" alt="up arrow" class="object-cover" />
    </div>
  </div>
</template>

<script>
import upArrow from '@/assets/icons/up_arrow.svg';

export default {
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      upArrow,
    };
  },
};
</script>

<style scoped>
.card-bag-color:hover {
  background: #F2F4F8;
}

.up-arrow-div {
  opacity: 0;
  transition: opacity 0.3s;
}

.card-bag-color:hover .up-arrow-div {
  opacity: 1;
}

/* Add ellipsis for overflowed text */
.truncate {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
</style>

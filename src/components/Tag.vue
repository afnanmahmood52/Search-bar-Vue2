<template>
  <div
    :class="[
      'rounded-full flex items-center cursor-pointer transition-colors',
      selected ? 'bg-blue-500 text-white' : 'bg-white text-blue-500'
    ]"
    @click="handleClick"
  >
    <div class="flex items-center gap-2 py-1 px-5 rounded-full"
      :class="{ 'tag-selected-bg-color': tag.selected, 'tag-unselected-bg-color': !tag.selected }"
    >
      <div
        class="transition-colors flex items-center justify-center"
        :class="{ 'text-white': tag.selected, 'text-blue-500': !tag.selected }"
        style="width: 16px; height: 16px;"
      >
        <img
          :src="!tag.selected ? require('@/assets/icons/blue_tag_icon.svg') : require('@/assets/icons/white_tag_icon.svg')"
          alt="icon"
          class="transition-colors"
          style="width: 100%; height: 100%;"
        />
      </div>
      <p 
        class="font-medium"
        :class="{ 'text-white': tag.selected, 'tag-unselected-text-color': !tag.selected }"
      >{{ tag.name }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    tag: {
      type: Object,
      required: true,
    },
    selected: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    handleClick() {
      this.$emit('click');
    },
  },
};
</script>

<style scoped>
.tag-unselected-bg-color {
  background: #F2F4F8;
}

.tag-selected-bg-color {
  background: #6833FF;
}

.tag-unselected-text-color {
  color: #6833FF;
}
</style>

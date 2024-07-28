<template>
  <div class="flex flex-wrap space-x-2">
    <Tag v-for="tag in tags" :key="tag.name" :tag="tag" :selected="tag.selected" @click="handleTagClick(tag.name)" />
  </div>
</template>

<script>
import Tag from './Tag.vue';

export default {
  components: {
    Tag,
  },
  props: {
    tags: {
      type: Array,
      required: true,
    },
  },
  methods: {
    handleTagClick(tagName) {
      this.$emit('tag-click', tagName);
    },
  },
};
</script>

<style scoped>
</style>

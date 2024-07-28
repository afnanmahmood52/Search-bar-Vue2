<template>
  <div class="card p-5 flex flex-col bg-white shadow-lg rounded-lg">
    <SearchBar :api_call_status="api_call_status" @search="handleSearch" @reset-tags="resetTags" :searchQuery="searchQuery" />
    <div class="py-5">
      <Tags :tags="tags" @tag-click="handleTagClick" />
    </div>
    <Items :items="filteredItems" :apiCallStatus="api_call_status" />
    <StatusSection :status_message="status_message" :api_call_status="api_call_status"/>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './SearchBar.vue';
import Tags from './Tags.vue';
import Items from './Items.vue';
import StatusSection from './StatusSection.vue';
import { API_STATUSES, STATUS_MESSAGE } from '../constants/constants';

export default {
  components: {
    SearchBar,
    Tags,
    Items,
    StatusSection,
  },
  data() {
    return {
      tags: [
        { name: 'Languages', selected: false },
        { name: 'Build', selected: false },
        { name: 'Design', selected: false },
        { name: 'Cloud', selected: false },
      ],
      filteredItems: [],
      api_call_status: API_STATUSES.SUCCESS,
      status_message: STATUS_MESSAGE.NO_RESULT,
      searchQuery: '',
    };
  },
  methods: {
    async handleSearch(query) {
      this.api_call_status = API_STATUSES.LOADING;
      this.status_message = STATUS_MESSAGE.SEARCHING;

      try {
        const response = await axios.get(`https://frontend-test-api.digitalcreative.cn/?no-throttling=false&search=${query}`);

        if (response.data && Array.isArray(response.data)) {
          this.filteredItems = response.data.map(item => ({
            title: item.title,
            description: item.description,
            image: item.image,
            url: item.url,
            category: item.category,
          }));

          if (this.filteredItems.length === 0) {
            this.status_message = STATUS_MESSAGE.NO_RESULT;
          } else {
            this.status_message = `${this.filteredItems.length} results`;
          }

          this.api_call_status = API_STATUSES.SUCCESS;
        } else {
          this.api_call_status = API_STATUSES.ERROR;
          this.status_message = STATUS_MESSAGE.ERROR;
        }
      } catch (error) {
        this.api_call_status = API_STATUSES.ERROR;
        this.status_message = STATUS_MESSAGE.ERROR;
      }
    },
    handleTagClick(tagName) {
      // Reset all tags to unselected and set the clicked tag as selected
      this.tags = this.tags.map(tag => ({
        ...tag,
        selected: tag.name === tagName
      }));
      this.searchQuery = tagName;
      this.handleSearch(tagName);
    },
    resetTags() {
      // Reset all tags to unselected when search is initiated
      this.tags = this.tags.map(tag => ({ ...tag, selected: false }));
    },
  },
};
</script>

<style scoped>
.card {
  box-shadow: 0 15px 24px rgba(0, 0, 0, 0.2), 0 8px 16px rgba(0, 0, 0, 0.2);
  max-width: 690px;
  min-width: 690px;
}
</style>

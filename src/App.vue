<template>
  <div id="app">
    <div
      class="flex items-center justify-center mt-48 lg:mt-0 lg:min-h-screen text-center main-container"
    >
    <MainComponent />
    </div>
  </div>
</template>

<script>
import MainComponent from "./components/MainComponent.vue";

export default {
  name: "App",
  components: {
    MainComponent,
  },
};
</script>

<style>
.main-container {
  background-color: #EDF2F7;
}
</style>

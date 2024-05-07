<template>
  <div id="app">
    <SearchBar @termChange="onTermChange"></SearchBar>
    <VideoList :videos="videos" @videoSelect="onVideoSelect"></VideoList>
  </div>
</template>

<script>
import SearchBar from "./components/SearchBar";
import VideoList from './components/VideoList';

export default {
  name: "App",
  components: {
    SearchBar,
    VideoList
  },
  data() {
    return {
      videos: []  // This will be populated by API response in the future
    }
  },
  methods: {
    onTermChange(searchTerm) {
      console.log('Search term changed:', searchTerm);
    },
    onVideoSelect(video) {
      console.log('Video selected:', video);
    }
  }
};
</script>

<style scoped>
</style>

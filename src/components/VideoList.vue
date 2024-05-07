<template>
  <ul class="list-group">
    <VideoListItem
     v-for="video in videos"
     :key="video.id"
     :video="video"
     @videoSelect="onVideoSelect">
    </VideoListItem>
  </ul>
</template>

<script>
import VideoListItem from './VideoListItem';

export default {
  name: "VideoList",
  props: {
    videos: Array
  },
  components: {
    VideoListItem
  },
  methods: {
    onVideoSelect(video) {
      this.$emit('videoSelect', video);
    }
  }
};
</script>

<style scoped>
</style>

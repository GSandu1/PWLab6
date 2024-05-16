<template>
    <div class="container">
      <h2>Liked Videos</h2>
      <div class="row">
        <div class="col-md-4" v-for="videoId in videoIds" :key="videoId">
          <iframe class="embed-responsive-item" :src="getVideoUrl(videoId)" allowfullscreen></iframe>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'LikedVideos',
    data() {
      return {
        videoIds: []
      };
    },
    mounted() {
      this.videoIds = JSON.parse(localStorage.getItem('likedVideos')) || [];
    },
    methods: {
      getVideoUrl(videoId) {
        return `https://www.youtube.com/embed/${videoId}`;
      }
    }
  };
  </script>
  
  <style>
  .embed-responsive-item {
    width: 100%;
    height: 200px; /* Set this according to your layout needs */
  }
  </style>
  
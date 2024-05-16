<template>
  <div id="app" class="container">
    <button @click="toggleTheme">Toggle Theme</button>
    <nav>
      <router-link to="/">Home</router-link>
      <router-link to="/likedvideos">Liked Videos</router-link>
    </nav>
    <router-view :videos="videos" :selectVideo="selectVideo" :handleUnlike="handleUnlike" 
                 @videoSelect="onVideoSelect" @termChange="fetchVideos">
    </router-view>
  </div>
</template>

<script>
import axios from "axios";

const API_KEY = 'AIzaSyCYKsZPI3YLGukHupLE2Mazc4tGbnxgp80';
const YOUTUBE_V3_URL = 'https://www.googleapis.com/youtube/v3/search';

export default {
  name: "App",
  data() {
    return {
      videos: [],
      selectVideo: null,
      darkTheme: false
    };
  },
  methods: {
    toggleTheme() {
      this.darkTheme = !this.darkTheme;
      document.body.className = this.darkTheme ? "dark-theme" : "";
    },
    fetchVideos(searchTerm) {
      axios.get(YOUTUBE_V3_URL, {
        params: {
          key: API_KEY,
          type: 'video',
          part: 'snippet',
          q: searchTerm
        }
      })
      .then(response => {
        this.videos = response.data.items;
      });
    },
    onVideoSelect(video) {
      this.selectVideo = video;
    },
    handleUnlike(videoId) {
      const likedVideos = JSON.parse(localStorage.getItem('likedVideos')) || [];
      const updatedLikedVideos = likedVideos.filter(id => id !== videoId);
      localStorage.setItem('likedVideos', JSON.stringify(updatedLikedVideos));
      this.fetchVideos();
    }
  }
};
</script>

<style>

:root {
  --background-color: #fff;
  --text-color: #000;
  --input-background: #fff;
  --input-text: #000;
}

/* Dark theme */
.dark-theme {
  --background-color: #333;
  --text-color: #fff;
  --input-background: #555;
  --input-text: #fff;
}

body {
  background-color: var(--background-color);
  color: var(--text-color);
}

input {
  background-color: var(--input-background);
  color: var(--input-text);
}

</style>
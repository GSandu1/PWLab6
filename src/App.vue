<template>
  <div id="app" class="container">
    <label class="switch">
      <input type="checkbox" @change="toggleTheme" :checked="darkTheme">
      <span class="slider round"></span>
    </label> 
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

.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  transition: .4s;
  border-radius: 34px;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  transition: .4s;
  border-radius: 50%;
}

input:checked + .slider {
  background-color: #2196F3;
}

input:focus + .slider {
  box-shadow: 0 0 1px #2196F3;
}

input:checked + .slider:before {
  transform: translateX(26px);
}

.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}

</style>
<template>
  <div id="app" class="container">
    <button @click="toggleTheme">Toggle Theme</button>
    <SearchBar @termChange="onTermChange"></SearchBar>
    <div class="row">
      <VideoDetail :video="selectVideo"></VideoDetail>
      <VideoList
      :videos="videos"
      @videoSelect="onVideoSelect">
      </VideoList>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar";
import VideoList from './components/VideoList';
import VideoDetail from './components/VideoDetail';

const API_KEY = '';
const YOUTUBE_V3_URL = 'https://www.googleapis.com/youtube/v3/search';
export default {
  name: "App",
  components: {
    SearchBar: SearchBar,
    VideoList: VideoList,
    VideoDetail: VideoDetail
  },
  data() {
    return {
      videos: [],
      selectVideo: null,
      darkTheme: false // Theme state
    }
  },
  methods: {
    toggleTheme() {
      this.darkTheme = !this.darkTheme;
      if (this.darkTheme) {
        document.body.classList.add("dark-theme");
      } else {
        document.body.classList.remove("dark-theme");
      }
    },
    onTermChange(searchTerm) {
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
      })
    },
    onVideoSelect(video) {
      this.selectVideo = Object.assign({}, video);  //immutable
    }
  }
};
</script>

<style >

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
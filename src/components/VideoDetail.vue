<template>
  <div v-if="video" class="col-md-8">
    <div class="embed-responsive embed-responsive-16by9">
      <iframe class="embed-responsive-item" :src="videoUrl" allowfullscreen></iframe>
    </div>
    <div class="detail">
      <h4>{{video.snippet.title}}</h4>
      <p>{{video.snippet.description}}</p>
      <button @click="likeVideo" class="btn btn-primary">Like</button>
    </div>
  </div>
</template>

<script>
const YOUTUBE_URL = "https://www.youtube.com/embed/";
export default {
  name: "VideoDetail",
  props: ["video"],
  computed: {
    videoUrl() {
      return `${YOUTUBE_URL}${this.video.id.videoId}`;
    }
  },
  methods: {
    likeVideo() {
      const likedVideos = JSON.parse(localStorage.getItem('likedVideos')) || [];
      if (!likedVideos.includes(this.video.id.videoId)) {
        likedVideos.push(this.video.id.videoId);
        localStorage.setItem('likedVideos', JSON.stringify(likedVideos));
        alert('Video liked!');
      } else {
        alert('You already liked this video!');
      }
    }
  }
};
</script>

<style scoped>
.detail {
  margin: 10px;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.btn-primary {
  margin-top: 10px;
}
</style>
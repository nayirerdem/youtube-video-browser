<template>
<div class="container">
    <h1 class="text-center">NagikhoTube</h1>
    <SearchBar @termChange="onTermChange"/>
    <div class="row">
        <div class="col-8">
            <VideoDetail :video="selectedVideo"/>
        </div>
        <div class="col-4">
            <VideoList :videos="videos" @videoSelect="onVideoSelect"/>
        </div>
    </div>
</div>
</template>
<script>
import SearchBar from "./components/SearchBar";
import VideoList from "./components/VideoList";
import VideoDetail from "./components/VideoDetail";
import axios from "axios";

const API_KEY = "";
const SEARCH_TERM = ""; 

export default {
  name: "App",
  data() {
    return {
      videos: [],
      selectedVideo: null
    };
  },
  components: {
    SearchBar,
    VideoList,
    VideoDetail
  },
  mounted() {
    this.getVideos();
  },
  methods: {
    onTermChange(searchTerm) {
      axios
        .get("https://www.googleapis.com/youtube/v3/search", {
          params: {
            key: API_KEY,
            type: "video",
            part: "snippet",
            maxResults: "10",
            q: searchTerm
          }
        })
        .then(response => {
          this.videos = response.data.items;
        });
    },
    onVideoSelect(video) {
      console.log(video);
      this.selectedVideo = video;
    }
  }
};
</script>
<style scoped>
h1 {
  color: cornflowerblue;
}
</style>


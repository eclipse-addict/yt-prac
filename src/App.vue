<template>
  <div id="app">
    <h1>First Youtube Project</h1>
    <TheSearchBar @input-change="onInputChange"/>
    <section>
      <VideoDetail :video="selectedVideo"/>
      <videoList :videos="videos" @select-video="onSelectVideo"/>
    </section>
  </div>
</template>

<script>
import axios from 'axios'
import TheSearchBar from "./components/TheSearchBar.vue"
import videoList from "./components/VideoList.vue"
import VideoDetail from "./components/VideoDetail.vue"


const API_KEY = "AIzaSyAr9AGZURj9-toddRHkxrAnbsJx35JcUhU"
const API_URL = 'https://www.googleapis.com/youtube/v3/search'

export default {
  name: 'App',
  data: function () {
    return {
      inputValue : null,
      videos: [],
      selectedVideo : null,
    }
  },
  components: {
    TheSearchBar,
    videoList,
    VideoDetail,
  },
  methods : {
    onInputChange: function (input) {
      // console.log('test',input);
      this.inputValue = input

      const params = {
        key: API_KEY,
        type: 'videos',
        part: 'snippet',
        q: this.inputValue,
      }
      
      axios({
        method: 'GET',
        url: API_URL,
        params,
      })
      .then(res => {
        // console.log('Result',res)
        this.videos = res.data.items
        console.log(this.videos)
      })
      .catch(err => {
        console.log('Error',err)
      });
    },
    onSelectVideo : function (video) {
      this.selectedVideo = video
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

<template>
  <div>
<ul>
    <VideoListItem 
      v-for="video in videos" 
      :key="video.id.videoId" 
      :video="video" 
      @select-video="onSelectVideo"
    />
  </ul>
  </div>
</template>

<script>
import VideoListItem from "@/components/VideoListItem.vue"
export default {
  name: 'videoList',
  props: {
    videos: {
      type: Array,
      required: true,
    }
  },
  components : {
    VideoListItem,
  },
  methods : {
    onSelectVideo: function (video) {
      this.$emit('select-video', video);
    }
  }
}
</script>

<style>

</style>
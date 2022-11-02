<template>
  <div>
    <li @click="selectVideo">
      <img :src="thumbnail" alt="youtub-thumbnail-img">
      <span v-html="video.snippet.title"></span>
    </li>
  </div>
</template>

<script>
export default {
  name: 'VideoListItem',
  props: {
    video: {
      type: Object,
      required: true
    }
  },
  computed :  {
    thumbnail: function () {
      return this.video.snippet.thumbnails.default.url
    }
  },
  methods : {
    selectVideo: function () {
      this.$emit('select-video', this.video)
    }
  }
}
</script>

<style>

</style>
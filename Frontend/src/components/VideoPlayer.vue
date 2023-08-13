<template>
  <div class="video-container">
    <video ref="videoPlayer" controls>
      <source :src="videoUrl" type="video/mp4" />
      <track
        label="English"
        kind="subtitles"
        :src="subtitlesUrl"
        srclang="en"
        default
      />
      Your browser does not support the video tag.
    </video>
  </div>
</template>

<script>
export default {
  props: ["video-url", "subtitles-url"],
  methods: {
    handleFileChange() {
      this.$refs.videoPlayer.load();
      // this.$refs.videoPlayer.play();
    },
  },
  watch: {
    videoUrl() {
      this.handleFileChange();
    },
  },
};
</script>

<style scoped>
.video-container {
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
  border: 1px solid #ccc;
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.1);
  padding: 15px;
  background-color: #f9f9f9;
  border-radius: 8px;
}

.video-container video {
  width: 100%;
  border-radius: 8px;
}

.video-container track {
  font-family: Arial, sans-serif;
  font-size: 14px;
  color: #333;
}
</style>

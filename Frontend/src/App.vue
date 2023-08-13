<template>
  <div id="app">
    <video-upload-form @file-uploaded="handleFileUploaded" />
    <video-player :video-url="videoUrl" :subtitles-url="subtitlesUrl" />
    <subtitle-editor @subtitle-updated="getSubtitle" />
  </div>
</template>

<script>
import VideoUploadForm from "@/components/VideoUploadForm.vue";
import VideoPlayer from "@/components/VideoPlayer.vue";
import SubtitleEditor from "@/components/SubtitleEditor.vue";
import axios from "axios";
export default {
  components: {
    VideoUploadForm,
    VideoPlayer,
    SubtitleEditor,
  },
  data() {
    return {
      videoUrl: "",
      subtitlesUrl: "",
    };
  },
  methods: {
    handleFileUploaded(file) {
      this.videoUrl = URL.createObjectURL(file);
      this.getSubtitle();
    },
    getSubtitle() {
      axios
        .get("http://127.0.0.1:8000/subtitles.vtt")
        .then((response) => {
          this.subtitlesUrl = URL.createObjectURL(
            new Blob([response.data], { type: "text/vtt" })
          );
        })
        .catch((error) => {
          console.error("Error fetching subtitles:", error);
        });
    },
  },
};
</script>

<style scoped>
.app-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background-color: #f4f4f4;
  font-family: Arial, sans-serif;
  padding: 20px;
}
</style>

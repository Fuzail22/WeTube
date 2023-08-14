<template>
  <div class="video-upload">
    <input type="file" @change="handleFileChange" accept="video/*" />
  </div>
</template>

<script>
import axios from "axios";

export default {
  // data() {
  //   return {
  //     sub: "",
  //   };
  // },
  methods: {
    handleFileChange(event) {
      const sub = "";
      event.preventDefault();
      const file = event.target.files[0];
      this.$emit("file-uploaded", file);
      const formData = new FormData();
      formData.append("file", file);
      axios
        .post("http://127.0.0.1:8000/upload/video", formData, {
          headers: {
            "Content-Type": "multipart/form-data",
          },
        })
        .then((response) => {
          console.log("Video uploaded successfully:", response.data);
        })
        .catch((error) => {
          console.error("Error uploading video:", error);
        });
      axios
        .post("http://127.0.0.1:8000/update-subtitles", {
          subtitlesContent: sub,
        })
        .then((response) => {
          console.log("Subtitles updated:", response.data);
          this.$emit("subtitle-updated");
        })
        .catch((error) => {
          console.error("Error updating subtitles:", error);
        });
    },
  },
};
</script>

<style scoped>
.video-upload {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
  border: 2px dashed #ccc;
  background-color: #f5f5f5;
  cursor: pointer;
  transition: border-color 0.3s ease-in-out;
}

.video-upload:hover {
  border-color: #888;
}
</style>

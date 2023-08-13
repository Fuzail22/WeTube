<template>
  <div class="container">
    <div class="subtitle-inputs">
      <input
        type="text"
        class="subtitle-inputs txt"
        v-model="newSubtitle.text"
      />
      <input
        type="time"
        class="subtitle-inputs"
        v-model="newSubtitle.startTime"
        step="1"
      />
      <input
        type="time"
        class="subtitle-inputs"
        v-model="newSubtitle.endTime"
        step="1"
      />
      <input
        type="button"
        class="add-button"
        value="Add Subtitle"
        @click="updateSubtitles"
      />
    </div>

    <div
      class="subtitle-item"
      v-for="(subtitle, index) in modifiedSubtitles"
      :key="index"
    >
      <span class="subtitle-time"
        >{{ subtitle.startTime }} - {{ subtitle.endTime }}:
      </span>
      <span class="subtitle-text">{{ subtitle.text }}</span>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      newSubtitle: {
        text: "",
        startTime: "00:00:00",
        endTime: "00:00:00",
      },
      subtitles: [],
      modifiedSubtitles: [],
    };
  },
  methods: {
    modifySubtitleFormat(subtitlesArray) {
      let modifiedContent = "WEBVTT\n\n";

      for (const subtitle of subtitlesArray) {
        modifiedContent += `${subtitle.startTime} --> ${subtitle.endTime}\n`;
        modifiedContent += `${subtitle.text}\n\n`;
      }
      axios
        .post("http://127.0.0.1:8000/update-subtitles", {
          subtitlesContent: modifiedContent,
        })
        .then((response) => {
          console.log("Subtitles updated:", response.data);
          this.$emit("subtitle-updated");
        })
        .catch((error) => {
          console.error("Error updating subtitles:", error);
        });
    },
    resetNewSubtitle() {
      this.newSubtitle.text = "";
      this.newSubtitle.startTime = "00:00:00";
      this.newSubtitle.endTime = "00:00:00";
    },
    formatTimeWithMilliseconds(prop) {
      if (this.newSubtitle[prop]) {
        this.newSubtitle[prop] = this.newSubtitle[prop] + ".000";
      }
    },
    updateSubtitles() {
      this.formatTimeWithMilliseconds("startTime");
      this.formatTimeWithMilliseconds("endTime");
      const existingSubtitle = this.subtitles.find(
        (subtitle) => subtitle.startTime === this.newSubtitle.startTime
      );

      if (existingSubtitle) {
        existingSubtitle.text = this.newSubtitle.text;
      } else {
        this.subtitles.push({ ...this.newSubtitle });
      }
      this.modifiedSubtitles = [...this.subtitles];
      this.resetNewSubtitle();
      this.modifySubtitleFormat(this.modifiedSubtitles);
    },
    fetchSubtitles() {
      axios
        .get("http://127.0.0.1:8000/subtitles.vtt")
        .then((response) => {
          console.log(response.data);
          this.subtitles = this.parseVTTContent(response.data);
          this.modifiedSubtitles = [...this.subtitles];
        })
        .catch((error) => {
          console.error("Error fetching subtitles:", error);
        });
    },
    parseVTTContent(content) {
      const lines = content.split(/\r?\n/);
      const subtitles = [];
      let currentSubtitle = {};

      for (const line of lines) {
        if (line.trim() === "") {
          if (
            currentSubtitle.startTime &&
            currentSubtitle.endTime &&
            currentSubtitle.text
          ) {
            subtitles.push({
              startTime: currentSubtitle.startTime,
              endTime: currentSubtitle.endTime,
              text: currentSubtitle.text,
            });
          }
          currentSubtitle = {};
        } else if (currentSubtitle.startTime) {
          if (!currentSubtitle.text) {
            currentSubtitle.text = line.trim();
          } else {
            currentSubtitle.text += " " + line.trim();
          }
        } else {
          const timecodes = line.split(" --> ");
          if (timecodes.length === 2) {
            currentSubtitle.startTime = timecodes[0];
            currentSubtitle.endTime = timecodes[1];
          }
        }
      }

      return subtitles;
    },
  },

  mounted() {
    this.fetchSubtitles();
  },
};
</script>
<style scoped>
.container {
  font-family: Arial, sans-serif;
  padding: 20px;
  align-content: center;
}

.subtitle-inputs {
  display: flex;
  gap: 10px;
  margin-bottom: 15px;
}

.subtitle-input {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.subtitle-input.txt {
  flex-grow: 1;
}

.add-button {
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  margin-bottom: 15px;
  padding: 8px 16px;
  cursor: pointer;
  transition: background-color 0.3s ease-in-out;
}

.add-button:hover {
  background-color: #0056b3;
}

.subtitle-item {
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 10px;
  margin-bottom: 10px;
  display: flex;
  align-items: center;
}

.subtitle-time {
  font-weight: bold;
  margin-right: 10px;
}

.subtitle-text {
  flex-grow: 1;
}
</style>

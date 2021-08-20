<template>
  <player :src="videoSrc" />

  <div style="display: flex; justify-content: space-between; margin-top: 1rem">
    <button
      v-for="(video, index) in videos"
      :key="index"
      @click="videoSrc = video"
      :class="videoSrc == video ? 'selected-video' : ''"
    >
      Video {{ index + 1 }}
    </button>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import Player from "./components/Player.vue";

const videos = [
  "https://file-examples-com.github.io/uploads/2017/04/file_example_MP4_480_1_5MG.mp4",
  "https://test-videos.co.uk/vids/bigbuckbunny/mp4/h264/1080/Big_Buck_Bunny_1080_10s_1MB.mp4",
];

export default defineComponent({
  name: "App",
  components: { Player },
  setup() {
    const videoSrc = ref(videos[0]);
    return { videoSrc, videos };
  },
});

Player;
</script>

<style scoped>
.selected-video {
  background-color: green;
}
</style>

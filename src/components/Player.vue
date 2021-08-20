<template>
  <video id="player" class="video-js"></video>
</template>

<script lang="ts">
import { defineComponent, onMounted, ref, onUnmounted, watch } from "vue";
import videojs, { VideoJsPlayer } from "video.js";
import "video.js/dist/video-js.css";

export default defineComponent({
  name: "VideoPlayer",
  props: {
    src: {
      type: String,
      required: true,
    },
  },
  setup(props) {
    var player = ref<VideoJsPlayer>();
    watch(
      () => props.src,
      (val) => {
        player.value?.loadMedia({ src: val, type: "video/mp4" }, () => {});
      }
    );
    onMounted(() => {
      player.value = videojs("player", {
        autoplay: true,
        controls: true,
        fluid: true,
        aspectRatio: "16:9",
        fill: true,
        sources: [
          {
            src: props.src,
            type: "video/mp4",
          },
        ],
      });
    });
    onUnmounted(() => {
      player.value?.dispose();
    });
    return {
      player,
    };
  },
});
</script>

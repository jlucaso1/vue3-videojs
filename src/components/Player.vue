<template>
  <video id="player" class="video-js"></video>
</template>

<script lang="ts">
import { defineComponent, onMounted, ref, onUnmounted, watch } from "vue";
// Type
import { VideoJsPlayer } from "video.js";
// Core lightweight version
import videojs from "video.js/dist/alt/video.core.novtt.js";
// Video.js css
import "video.js/dist/video-js.min.css";

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
        //Reload video source
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

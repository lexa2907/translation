<template>
    <div ref="artRef"></div>
  </template>
  
  <script>
  import Artplayer from "artplayer";
  import Hls from "hls.js"

  function playM3u8(video, url, art) {
    if (Hls.isSupported()) {
        if (art.hls) art.hls.destroy();
        const hls = new Hls();
        hls.loadSource(url);
        hls.attachMedia(video);
        art.hls = hls;
        art.on('destroy', () => hls.destroy());
    } else if (video.canPlayType('application/vnd.apple.mpegurl')) {
        video.src = url;
    } else {
        art.notice.show = 'Unsupported playback format: m3u8';
    }
}
  
  export default {
    data() {
      return {
        instance: null,
      };
    },
    props: {
      option: {
        type: Object,
        required: true,
      },
    },
    mounted() {
      this.instance = new Artplayer({
        ...this.option,
        container: this.$refs.artRef,
        fullscreen: true,
        isLive: true,
        type: 'm3u8',
    customType: {
        m3u8: playM3u8,
    },
      });
  
      this.$nextTick(() => {
        this.$emit("get-instance", this.instance);
      });
    },
    beforeUnmount() {
      if (this.instance && this.instance.destroy) {
        this.instance.destroy(false);
      }
    },
  };
  </script>
<template>
  <section class="container">
    <div>
      <h1>pages/with-custom-button.vue</h1>
      <p>using custom continue button</p>
      <div class="video">
        <video-mark
          ref="videoMark"
          src="/big_buck_bunny.mp4"
          :rootAttrs="{style:{width:'360px',height:'203px',position:'relative'}}"
          v-on:mark="addMark"
        >
          <button v-on:click="hideVideoEditor">[continue]</button>
        </video-mark>
      </div>
    </div>
  </section>
</template>

<script>
import VideoMark from "vue-video-mark/VideoMark.vue";

export default {
  components: {
    VideoMark
  },
  methods: {
    addMark: function(mark) {
      alert(
        `start=${JSON.stringify(mark.start)} width:${mark.width} height:${
          mark.height
        }`
      );
      console.log(mark);
    },
    hideVideoEditor: function() {
      this.$refs.videoMark.hideEditor();
    }
  }
};
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
</style>

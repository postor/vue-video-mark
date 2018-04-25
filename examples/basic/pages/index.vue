<template>
  <section class="container">
    <div>
      <h1>pages/index.vue</h1>
      <p>pause video and draw mark an area, and see the result<br>full result in console</p>
      <div class="video">
        <video-mark
          src="/big_buck_bunny.mp4"
          :rootAttrs="{style:{width:'360px',height:'203px',position:'relative'}}"
          v-on:mark="addMark"
        >
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

<template>
  <section class="container">
    <div>
      <h1>pages/show.vue</h1>
      <p>show the mark you made <br> 
      just lay a mark on a image <br>
      you can use your own component <br>
      instead of vue-video-mark/VideoMarkView.vue</p>
      <div class="video">
        <video-mark
          src="/big_buck_bunny.mp4"
          :rootAttrs="{style:{width:'360px',height:'203px',position:'relative'}}"
          v-on:mark="addMark"
        >
        </video-mark>
      </div>
      <video-mark-view
        v-if="mark"
        :mark="mark"
        :rootAttrs="{style:{width:'360px',height:'203px',position:'relative'}}"
      ></video-mark-view>
    </div>
  </section>
</template>

<script>
import VideoMark from "vue-video-mark/VideoMark.vue";
import VideoMarkView from "vue-video-mark/VideoMarkView.vue";

export default {
  components: {
    VideoMark,
    VideoMarkView
  },
  data: () => ({
    mark: undefined
  }),
  methods: {
    addMark: function(mark) {
      this.mark = mark;
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

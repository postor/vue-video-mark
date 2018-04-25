<template>
  <section class="container">
    <h1>pages/full.vue</h1>
    <div class="video">
      <video-mark
        ref="videoMark"
        src="/big_buck_bunny.mp4"
        :rootAttrs="videoRootAttrs"
        :markAttrs="{style:{borderColor:'blue'}}"
        v-on:mark="addMark"
      >
        <button v-on:click="hideVideoEditor">[继续播放]</button>
      </video-mark>
    </div>
    <div class="views">
      <video-mark-view
        v-for="(mark,i) in marks"
        v-bind:key="i"
        :rootAttrs="viewRootAttrs"
        :markAttrs="{style:{borderColor:'green'}}"
        :mark="mark"
      ></video-mark-view>
    </div>
  </section>
</template>

<script>
import VideoMark from "vue-video-mark/VideoMark.vue";
import VideoMarkView from "vue-video-mark/VideoMarkView.vue"

export default {
  components: {
    VideoMark,
    VideoMarkView
  },
  data: () => {
    return {
      video: {
        width: 360,
        height: 203
      },
      marks: []
    };
  },
  methods: {
    addMark: function(mark) {
      this.marks = [mark].concat(this.marks);
    },
    hideVideoEditor: function() {
      this.$refs.videoMark.hideEditor();
    }
  },
  computed: {
    videoRootAttrs: function() {
      return {
        style: {
          border: "1px solid red",
          width: `${this.video.width}px`,
          height: `${this.video.height}px`,
          margin: "0 auto",
          position: "relative"
        }
      };
    },
    viewRootAttrs: function() {
      return {
        style: {
          border: "1px solid red",
          width: `${this.video.width / 2}px`,
          height: `${this.video.height / 2}px`,
          margin: "0 auto",
          position: "relative"
        }
      };
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

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

.video,
.views {
  float: left;
  padding: 5px;
}
</style>

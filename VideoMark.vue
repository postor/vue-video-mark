<template>
  <div v-bind="rootAttrs">
    <video 
      ref="video" 
      :src="src" 
      controls 
      autoplay 
      v-on:pause="showEditor" 
      v-on:play="hideEditor" />
    <div ref="editor" class="editor" v-show="showing">
      <img 
        ref="img"
        :src="imgSrc" 
        v-on:mousedown="beginDrawing" 
        v-on:mousemove="resizeDrawing" 
        v-on:mouseup="endDrawing" 
        />
      <div class="mark" v-show="drawing" v-bind="markAttrs" :style="markStyle" ></div>
      <slot>
        <button v-on:click="hideEditor">continue</button>
      </slot>      
    </div>
  </div>  
</template>

<script>
import captureVideoFrame from "capture-video-frame";
import $ from "jquery";

export default {
  props: ["rootAttrs", "src", "markAttrs"],
  data: () => ({
    startPoint: {
      x: 0,
      y: 0
    },
    endPoint: {
      x: 0,
      y: 0
    },
    imgPosition: {
      x: 0,
      y: 0
    },
    text: "",
    drawing: false,
    showing: false,
    imgSrc: "about:blank"
  }),
  methods: {
    showEditor: function() {
      this.showing = true;
      const frame = captureVideoFrame(this.$refs.video, "png");
      this.imgSrc = frame.dataUri;
    },
    hideEditor: function() {
      this.showing = false;
      this.$refs.video.play();
    },
    beginDrawing: function(e) {
      e.preventDefault();
      this.drawing = true;
      const pos = $(this.$refs.editor).offset();
      this.imgPosition = {
        x: pos.left,
        y: pos.top
      };
      this.startPoint = {
        x: e.pageX,
        y: e.pageY
      };
      this.endPoint = this.startPoint;
    },
    resizeDrawing: function(e) {
      e.preventDefault();
      if (!this.drawing) {
        return;
      }
      this.endPoint = {
        x: e.pageX,
        y: e.pageY
      };
    },
    endDrawing: function(e) {
      e.preventDefault();
      this.drawing = false;

      const start = this.getOffset(this.startPoint, this.imgPosition);
      const widthHeight = this.getOffset(this.endPoint, this.startPoint);
      const widthHeightParent = {
        x: $(this.$refs.editor).width(),
        y: $(this.$refs.editor).height()
      };
      const widthHeightPercentage = this.getPercentage(
        widthHeight,
        widthHeightParent
      );
      const result = {
        start,
        width: widthHeight.x,
        height: widthHeight.y,
        percentage: {
          start: this.getPercentage(start, widthHeightParent),
          width: widthHeightPercentage.x,
          height: widthHeightPercentage.y
        },
        time: this.$refs.video.currentTime,
        imgSrc: this.imgSrc
      };
      this.$emit("mark", result);
    },
    getOffset(a, b) {
      return {
        x: a.x - b.x,
        y: a.y - b.y
      };
    },
    getPercentage(a, b) {
      return {
        x: a.x / b.x,
        y: a.y / b.y
      };
    }
  },
  computed: {
    markStyle: function() {
      const startOffset = this.getOffset(this.startPoint, this.imgPosition);
      const widthHeight = this.getOffset(this.endPoint, this.startPoint);
      const currentStyle = (this.markAttrs && this.markAttrs.style) || {};
      return {
        ...currentStyle,
        top: `${startOffset.y}px`,
        left: `${startOffset.x}px`,
        width: `${widthHeight.x}px`,
        height: `${widthHeight.y}px`
      };
    }
  }
};
</script>

<style>
video,
canvas,
img,
.editor {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
}

.editor {
  background-color: rgba(0, 0, 0, 0.2);
}

button {
  position: absolute;
  bottom: 0;
  right: 0;
}

img {
  cursor: crosshair;
}

.mark {
  position: absolute;
  border: 4px solid red;
  border-radius: 100%;
}
</style>

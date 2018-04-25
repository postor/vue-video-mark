<template>
  <div>
    <p>{{mark.time}}秒</p>
    <div v-bind="rootAttrs">    
      <img :src="mark.imgSrc" />
      <div class="mark" v-bind="markAttrs||{}" :style="markStyle" ></div>
    </div>  
  </div>
</template>

<script>
export default {
  props: ["rootAttrs", "mark", "markAttrs"],
  computed: {
    markStyle: function() {
      const percentage = this.mark.percentage;
      const currentStyle = (this.markAttrs && this.markAttrs.style) || {};
      return {
        ...currentStyle,
        top: `${percentage.start.y * 100}%`,
        left: `${percentage.start.x * 100}%`,
        width: `${percentage.width * 100}%`,
        height: `${percentage.height * 100}%`
      };
    }
  }
};
</script>

<style>
img {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  cursor: crosshair;
}

.mark {
  position: absolute;
  border: 4px solid red;
  border-radius: 100%;
}
</style>

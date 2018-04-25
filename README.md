# vue-video-mark

vue视频标记组件 | video mark component for vue

## 使用 | usage

### 基础 | basic

```
<template>
   <video-mark
        src="/big_buck_bunny.mp4"
        :rootAttrs="{style:{width:'360px',height:'203px',position:'relative'}}"
        v-on:mark="addMark"
    >
    </video-mark>
</template>

<script>
import VideoMark from "vue-video-mark/VideoMark.vue";

export default {
  components: {
    VideoMark
  },
  methods: {
    addMark: function(mark) {
      console.log(mark);
    }
  }
};
</script>
```

[./examples/basic/pages/index.vue](./examples/basic/pages/index.vue)

### 自定义继续按钮 | custom continue button

```
<template>
  <video-mark
    ref="videoMark"
    ...
  >
    <button v-on:click="hideVideoEditor">[my continue]</button>
  </video-mark>
</template>

<script>
import VideoMark from "vue-video-mark/VideoMark.vue";
export default {
  ...
  methods: {
    ...
    hideVideoEditor: function() {
      this.$refs.videoMark.hideEditor();
    }
  }
};
</script>
```
[./examples/basic/pages/with-custom-button.vue](./examples/basic/pages/with-custom-button.vue)

### 自定义标记样式 | custom mark style

```
<template>
  <video-mark
    :markAttrs="{style:{borderColor:'green'}}"
    ...
  >
  </video-mark>
</template>
```
[./examples/basic/pages/with-custom-mark.vue](./examples/basic/pages/with-custom-mark.vue)


### 显示标记 | show the mark

```
<video-mark-view
  :mark="mark"
  :rootAttrs="{style:{width:'360px',height:'203px',position:'relative'}}"
></video-mark-view>
```

[./examples/basic/pages/show.vue](./examples/basic/pages/show.vue)

### 综合使用 | full example

[./examples/basic/pages/full.vue](./examples/basic/pages/full.vue)

## 运行示例 | try it out

```
$ cd examples/basic

# install dependencies
$ npm install # Or yarn install

# serve with hot reload at localhost:3000
$ npm run dev
```

然后打开 | then open 

- http://localhost/
- http://localhost/with-custom-button
- http://localhost/with-custom-mark
- http://localhost/show
- http://localhost/full
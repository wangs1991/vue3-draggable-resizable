<template>
  <div id="app">
    <div>
      x:{{ x }}
      <button @click="x += 10">+</button>
      <button @click="x -= 10">-</button>
    </div>
    <div>
      y:{{ y }}
      <button @click="y += 10">+</button>
      <button @click="y -= 10">-</button>
    </div>
    <div>
      w:{{ w }}
      <button @click="w += 10">+</button>
      <button @click="w -= 10">-</button>
    </div>
    <div>
      h: {{ h }}
      <button @click="h += 10">+</button>
      <button @click="h -= 10">-</button>
    </div>
    <div>
      active:{{ active }}
      <br />
    </div>
    <div class="parent">
      <Vue3DraggableResizable
        :initW="300"
        :initH="250"
        v-model:x="x"
        v-model:y="y"
        v-model:w="w"
        v-model:h="h"
        v-model:active="active"
        :draggable="draggable"
        :resizable="resizable"
        :parent="true"
        :disabledX="false"
        :disabledW="false"
        :disabledH="false"
        :disabledY="false"
        :lockAspectRatio="true"
        :minW="200"
        :minH="50"
        classNameHandle="my-handle"
        @activated="print('activated')"
        @deactivated="print('deactivated')"
        @drag-start="print('drag-start', $event)"
        @resize-start="print('resize-start', $event)"
        @dragging="print('dragging', $event)"
        @resizing="print('resizing', $event)"
        @drag-end="print('drag-end', $event)"
        @resize-end="print('resize-end', $event)"
      >
        <template #header style="background: #f00;">header</template>
        This is a test example
        <button @click="test">内部事件</button>
      </Vue3DraggableResizable>

    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Vue3DraggableResizable from './components/Vue3DraggableResizable'
import DraggableContainer from './components/DraggableContainer'

export default defineComponent({
  components: { DraggableContainer, Vue3DraggableResizable },
  data() {
    return {
      x: 10,
      y: 10,
      h: 250,
      w: 300,
      active: false,
      draggable: true,
      resizable: true
    }
  },
  mounted() {
    setTimeout(() => {
      this.w = 50
    }, 3000)
  },
  methods: {
    print(val: any, e: any) {
      // console.log(val, e)
    },
    test() {
      alert()
    }
  }
})
</script>
<style lang="less" scoped>
.parent {
  width: 100%;
  height: 800px;
  // position: absolute;
  // top: 100px;
  // left: 200px;
  position: relative;
  border: 1px solid #000;
  user-select: none;
  ::v-deep {
    .vdr-container {
      border-color: #999;
    }
  }
}
</style>

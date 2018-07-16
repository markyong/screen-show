<template>
  <div style="width: 100%; height: 100%">
    <!--<div @dragover="dragover($event)" v-for="item in row" :key="item" :style="{width: rowWidth + '%', height: rowHeight + '%'}">-->
      <!--<div style="display: inline-block" @drop="drop($event)" data-gs-x="0" data-gs-y="0" data-gs-width="4" data-gs-height="2" class="grid-stack-item" v-for="item in span" :key="item" :style="{width: spanWidth + '%', height: spanHeight + '%'}">-->
        <!--<div class="boxStyle"></div>-->
      <!--</div>-->
    <!--</div>-->
    <grid-layout
      :layout="layout"
      :col-num="rowSpan.span"
      :row-height="rowSpan.rowHeight"
      :is-draggable="true"
      :is-resizable="true"
      :vertical-compact="true"
      :margin="[0,0]"
      :use-css-transforms="true"
    >

      <grid-item v-for="item in layout"
                 :key="item.i"
                 :x="item.x"
                 :y="item.y"
                 :w="item.w"
                 :h="item.h"
                 :i="item.i"
                 :style="item.style">
        {{item.i}}
      </grid-item>
    </grid-layout>
  </div>
</template>
<script>
import VueGridLayout from 'vue-grid-layout'
var GridLayout = VueGridLayout.GridLayout
var GridItem = VueGridLayout.GridItem
export default {
  name: 'SsContent',
  data () {
    return {
      rowWidth: 100,
      rowHeight1: 100,
      spanWidth: 100,
      spanHeight: 100,
      layout: []
    }
  },
  components: {
    GridLayout,
    GridItem
  },
  props: {
    span: {
      type: Number,
      default: 1
    },
    row: {
      type: Number,
      default: 1
    },
    rowHeight: {
      type: Number,
      default: 0
    },
    rowSpan: {
      type: Object
    }
  },
  watch: {
    rowSpan: {
      deep: true,
      handler: function (val) {
        this.layout = []
        let k = 1
        for (let i = 0; i < val.row; i++) {
          for (let j = 0; j < val.span; j++) {
            this.layout.push({x: j, y: i, w: 1, h: 1, i: k++, style: {background: `rgba(${Math.random() * 255}, ${Math.random() * 255}, ${Math.random() * 255}, 0.4)`}})
          }
        }
      }
    }
  },
  methods: {
    drop (e) {
      let data = e.dataTransfer.getData('text')
      console.log(e)
      e.target.appendChild(document.getElementById(data))
    },
    dragover (e) {
      e.preventDefault()
    }
  }
}
</script>
<style scoped>
  .boxStyle {
    border: 1px solid red;
    display: inline-block;
    box-sizing: border-box;
    width: 100%;
    height: 100%;
    display: inline-block;
  }
  div {
    box-sizing: border-box;
  }
  #content {
    width: 100%;
  }
  .vue-grid-layout {
    background: #eee;
  }
  .layoutJSON {
    background: #ddd;
    margin-top: 10px;
    padding: 10px;
  }
  .eventsJSON {
    background: #ddd;
    margin-top: 10px;
    padding: 10px;
    height: 100px;
    overflow-y: scroll;
  }
  .columns {
    -moz-columns: 120px;
    -webkit-columns: 120px;
    columns: 120px;
  }
  .vue-resizable-handle {
    z-index: 5000;
    position: absolute;
    width: 20px;
    height: 20px;
    bottom: 0;
    right: 0;
    background: url('data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBzdGFuZGFsb25lPSJubyI/Pg08IS0tIEdlbmVyYXRvcjogQWRvYmUgRmlyZXdvcmtzIENTNiwgRXhwb3J0IFNWRyBFeHRlbnNpb24gYnkgQWFyb24gQmVhbGwgKGh0dHA6Ly9maXJld29ya3MuYWJlYWxsLmNvbSkgLiBWZXJzaW9uOiAwLjYuMSAgLS0+DTwhRE9DVFlQRSBzdmcgUFVCTElDICItLy9XM0MvL0RURCBTVkcgMS4xLy9FTiIgImh0dHA6Ly93d3cudzMub3JnL0dyYXBoaWNzL1NWRy8xLjEvRFREL3N2ZzExLmR0ZCI+DTxzdmcgaWQ9IlVudGl0bGVkLVBhZ2UlMjAxIiB2aWV3Qm94PSIwIDAgNiA2IiBzdHlsZT0iYmFja2dyb3VuZC1jb2xvcjojZmZmZmZmMDAiIHZlcnNpb249IjEuMSINCXhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiIHhtbDpzcGFjZT0icHJlc2VydmUiDQl4PSIwcHgiIHk9IjBweCIgd2lkdGg9IjZweCIgaGVpZ2h0PSI2cHgiDT4NCTxnIG9wYWNpdHk9IjAuMzAyIj4NCQk8cGF0aCBkPSJNIDYgNiBMIDAgNiBMIDAgNC4yIEwgNCA0LjIgTCA0LjIgNC4yIEwgNC4yIDAgTCA2IDAgTCA2IDYgTCA2IDYgWiIgZmlsbD0iIzAwMDAwMCIvPg0JPC9nPg08L3N2Zz4=');
    background-position: bottom right;
    padding: 0 3px 3px 0;
    background-repeat: no-repeat;
    background-origin: content-box;
    box-sizing: border-box;
    cursor: se-resize;
  }
  .vue-grid-item:not(.vue-grid-placeholder) {
    background: #ccc;
    /*border: 1px solid black;*/
  }
  .vue-grid-item.resizing {
    opacity: 0.9;
  }
  .vue-grid-item.static {
    background: #cce;
  }
  .vue-grid-item .text {
    font-size: 24px;
    text-align: center;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    margin: auto;
    height: 100%;
    width: 100%;
  }
  .vue-grid-item .no-drag {
    height: 100%;
    width: 100%;
  }
  .vue-grid-item .minMax {
    font-size: 12px;
  }
  .vue-grid-item .add {
    cursor: pointer;
  }
  .vue-draggable-handle {
    position: absolute;
    width: 20px;
    height: 20px;
    top: 0;
    left: 0;
    background: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='10' height='10'><circle cx='5' cy='5' r='5' fill='#999999'/></svg>") no-repeat;
    background-position: bottom right;
    padding: 0 8px 8px 0;
    background-repeat: no-repeat;
    background-origin: content-box;
    box-sizing: border-box;
    cursor: pointer;
  }
</style>

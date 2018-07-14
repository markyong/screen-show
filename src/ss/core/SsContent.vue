<template>
  <div style="width: 100%; height: 100%">
    <div v-for="item in row" :key="item" :style="{width: rowWidth + '%', height: rowHeight + '%'}">
      <div class="boxStyle" v-for="item in span" :key="item" :style="{width: spanWidth + '%', height: spanHeight + '%'}"></div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'SsContent',
  data () {
    return {
      rowWidth: 100,
      rowHeight: 100,
      spanWidth: 100,
      spanHeight: 100
    }
  },
  props: {
    span: {
      type: Number,
      default: 1
    },
    row: {
      type: Number,
      default: 1
    }
  },
  mounted () {
  },
  watch: {
    row (val) {
      this.rowHeight = 100 / val
    },
    span (val) {
      this.spanWidth = 100 / val
    }
  }
}
</script>
<style scoped>
  .boxStyle {
    border: 1px solid red;
    display: inline-block;
    box-sizing: border-box;
  }
</style>

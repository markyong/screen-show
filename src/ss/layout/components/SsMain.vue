<template>
  <el-container>
    <ss-content :row-span="rowSpan"></ss-content>
  </el-container>
</template>
<script>
import SsContent from '../../core/SsContent.vue'
export default {
  name: 'SsMain',
  mounted () {
    const self = this
    let innerHeight = window.innerHeight
    this.$el.style.height = innerHeight + 'px'
    this.$root.Bus.$on('WAH', function (data) {
      self.rowSpan.span = data[0]
      self.rowSpan.row = data[1]
      self.rowSpan.rowHeight = innerHeight / data[1]
    })
  },
  data () {
    return {
      rowSpan: {
        row: 1,
        span: 1,
        rowHeight: 0
      }
    }
  },
  components: {
    SsContent
  }
}
</script>
<style scoped>
  .el-container {
    overflow: hidden;
  }
</style>

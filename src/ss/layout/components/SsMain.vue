<template>
  <el-container>
    <ss-content :row="row" :span="col"></ss-content>
  </el-container>
</template>
<script>
import SsContent from '../../core/SsContent.vue'
export default {
  name: 'SsMain',
  mounted () {
    const self = this
    this.$el.style.height = window.innerHeight + 'px'
    this.$root.Bus.$on('WAH', function (data) {
      self.col = data[0]
      self.row = data[1]
      console.log(data)
    })
  },
  data () {
    return {
      row: 1,
      col: 1
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
    background: #232E1C;
  }
</style>

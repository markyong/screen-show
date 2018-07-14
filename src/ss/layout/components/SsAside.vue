<template>
  <el-aside>
    <div class="inputNum">
      <span>宽度：</span><el-input-number size="small" v-model="widthCount" :min="1" :max="10" style="width: 97px"></el-input-number>
      <span>高度：</span><el-input-number size="small" v-model="heightCount" :min="1" :max="10" style="width: 97px"></el-input-number>
    </div>
    <div class="btn">
      <el-button size="small" @click="reset">重置</el-button>
      <el-button size="small" type="primary" @click="confirm">确认</el-button>
    </div>
  </el-aside>
</template>
<script>
export default {
  name: 'SsAside',
  data () {
    return {
      widthCount: 1,
      heightCount: 1
    }
  },
  methods: {
    reset () {
      this.widthCount = 1
      this.heightCount = 1
      this.$root.Bus.$emit('WAH', [this.widthCount, this.heightCount])
    },
    confirm () {
      this.$root.Bus.$emit('WAH', [this.widthCount, this.heightCount])
    }
  }
}
</script>
<style scoped>
  .el-aside {
    float: left;
    height: 500px;
    background: rgba(0,0,0,0.7);
  }
  .inputNum {
    height: 47px;
    line-height: 47px;
  }
  .btn {
    text-align: center;
    height: 47px;
    line-height: 47px;
  }
</style>

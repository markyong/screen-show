<template>
  <div>
    <SsAside></SsAside>
    <SsMain></SsMain>
  </div>
</template>
<script>
import SsAside from './components/SsAside.vue'
import SsMain from './components/SsMain.vue'
export default {
  name: 'Layout',
  components: {
    SsAside,
    SsMain
  }
}
</script>
<style>

</style>

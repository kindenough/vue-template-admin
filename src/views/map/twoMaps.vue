<template>
  <div style="width: 100%;">
    <div
      style="position: absolute;left: 2px;top: 2px;background-color: white;width:50%;height: 100%;"
    >
      <google1/>
    </div>
    <div
      style="position: absolute;right: 2px;top: 2px;background-color: white;width:50%;height: 100%;"
    >
      <google2/>
    </div>

  </div>
</template>

<script>
  import google1 from './google1'
  import google2 from './google2'

  export default {
    components: {
      google1,
      google2
    },
    // data() {
    //   return {
    //     zoom: 10,
    //     center: [118, 24.5],
    //     state: true
    //   }
    // },
    // methods: {
    //   setZoom() {
    //     this.zoom = this.zoom + 1
    //     this.center = [118.5, 24.7]
    //     this.state = true
    //   },
    // }
  }
</script>

<style scoped>

</style>

<template>
  <div id="map" class="map" />
</template>

<script>

import Map from 'ol/Map.js'
import View from 'ol/View.js'
import TileLayer from 'ol/layer/Tile.js'
import XYZ from 'ol/source/XYZ.js'

export default {
  name: 'Google',
  mounted() {
    this.initGoogle()
  },
  methods: {
    // initOL() {
    //   var attribution = new Attribution({
    //     collapsible: false
    //   })
    //   var map = new Map({
    //     layers: [
    //       new TileLayer({
    //         source: new XYZ({
    //           url: 'http://localhost:8999/{z}/{y}/{x}.png'
    //         })
    //       })
    //     ],
    //     controls: defaultControls({ attribution: false }).extend([attribution]),
    //     target: 'map',
    //     view: new View({
    //       center: [0, 0],
    //       zoom: 2
    //     })
    //   })
    //
    //   function checkSize() {
    //     var small = map.getSize()[0] < 600
    //     attribution.setCollapsible(small)
    //     attribution.setCollapsed(small)
    //   }
    //
    //   window.addEventListener('resize', checkSize)
    //   checkSize()
    // },
    // initTDT() {
    //   const map = new T.Map('map')
    //   map.centerAndZoom(new T.LngLat(118.20769, 24.4345), 11)
    //
    //   // 创建对象
    //   var ctrl = new T.Control.MapType()
    //   // 添加控件
    //   map.addControl(ctrl)
    // },
    initGoogle() {
      // eslint-disable-next-line no-unused-vars
      var map = new Map({
        target: 'map',
        layers: [
          new TileLayer({
            source: new XYZ({
              url:
                'http://mt3.google.cn/vt/lyrs=m@257000000,highlight:0x3414f2f5d748efc3:0x41be0725d8ddcbd0@1%7Cstyle:maps&hl=zh-CN&gl=CN&src=app&s=Ga&x={x}&y={y}&z={z}'
            })
          })
        ],
        // view: new View({
        //   center: [118.180530, 24.485920],
        //   zoom: 16
        // })
        view: new View({
          center: [118.180530,24.485920],
          projection: 'EPSG:4326',
          zoom: 10
        })
      })
    }
  }
}

</script>

<style scoped>
  .map {
    width: 100%;
    height:100vh;
  }
</style>

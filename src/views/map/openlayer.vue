<template>
  <div id="map" class="map" />
</template>

<script>
import 'ol/ol.css'
import Map from 'ol/Map'
import View from 'ol/View'
import { defaults as defaultControls, Attribution } from 'ol/control'
import TileLayer from 'ol/layer/Tile'
import OSM from 'ol/source/OSM'

export default {
  name: 'Index',
  mounted() {
    this.initTDT()
  },
  methods: {
    initOL() {
      var attribution = new Attribution({
        collapsible: false
      })
      var map = new Map({
        layers: [
          new TileLayer({
            source: new OSM()
          })
        ],
        controls: defaultControls({ attribution: false }).extend([attribution]),
        target: 'map',
        view: new View({
          center: [0, 0],
          zoom: 2
        })
      })

      function checkSize() {
        var small = map.getSize()[0] < 600
        attribution.setCollapsible(small)
        attribution.setCollapsed(small)
      }

      window.addEventListener('resize', checkSize)
      checkSize()
    },
    initTDT() {
      const map = new T.Map('map')
      map.centerAndZoom(new T.LngLat(118.20769, 24.4345), 11)

      // 创建对象
      var ctrl = new T.Control.MapType()
      // 添加控件
      map.addControl(ctrl)
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

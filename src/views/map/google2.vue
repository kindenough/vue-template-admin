<template>
  <div id="map2" class="map" />
</template>

<script>

import Map from 'ol/Map.js'
import View from 'ol/View.js'
import TileLayer from 'ol/layer/Tile.js'
import XYZ from 'ol/source/XYZ.js'
import bus from '../../utils/bus.js'

import 'ol/ol.css'
import Feature from 'ol/Feature'
import Overlay from 'ol/Overlay'
import Point from 'ol/geom/Point'
import { Vector as VectorLayer } from 'ol/layer'
import TileJSON from 'ol/source/TileJSON'
import VectorSource from 'ol/source/Vector'
import { Icon, Style } from 'ol/style'
export default {
  name: 'Google',
  data() {
    return {
      map: null
    }
  },
  mounted() {
    this.initGoogle()
  },
  methods: {

    initGoogle() {
      // eslint-disable-next-line no-unused-vars
      var map = new Map({
        target: 'map2',
        layers: [
          new TileLayer({
            source: new XYZ({
              url:
              // 'http://mt3.google.cn/vt/lyrs=s@169&hl=zh-CN&gl=CN&src=app&s=G&x={x}&y={y}&z={z}'
                  'http://mt3.google.cn/vt/lyrs=s@169,highlight:0x3414f2f5d748efc3:0x41be0725d8ddcbd0@1%7Cstyle:maps&hl=zh-CN&gl=CN&src=app&s=G&x={x}&y={y}&z={z}'
              // 'http://localhost:8999/{z}/{y}/{x}.png'
            })
          })
        ],
        // view: new View({
        //   center: [118.180530, 24.485920],
        //   zoom: 16
        // })
        view: new View({
          center: [118.180530, 24.485920],
          projection: 'EPSG:4326',
          zoom: 17
        })
      })

      this.addVectorLayer(map)

      map.on('moveend', function() {
        // eslint-disable-next-line no-undef
        var zoom = map.getView().getZoom()
        var center = map.getView().getCenter()
        // alert(zoom + '\n' + center)
        var obj = {}
        obj.zoom = zoom
        obj.center = center
        bus.$emit('listenMap2', obj)
      })

      this.mapOnClick(map)
      this.map = map

      var _this = this
      bus.$on('listenMap1', function(obj) {
        if (obj.zoom == null) {
          _this.setPtIcon(map, obj.center)
        } else {
          if (obj.zoom == map.getView().getZoom() &&
            obj.center == map.getView().getCenter()) {
            return
          }
          map.getView().setZoom(obj.zoom)
          map.getView().setCenter(obj.center)
        }
      })
    },
    setPtIcon(map, coordinate) {
      map.getLayers().getArray().forEach(function(e, idx) {
        if (idx == 1) {
          const layer = e
          const source = layer.getSource()
          const feat = source.getFeatures()[0]
          feat.setGeometry(new
          Point(coordinate))
        }
      })
    },
    mapOnClick(map) {
      var _this = this
      map.on('click', function(evt) {
        debugger
        _this.setPtIcon(map, evt.coordinate)
      })
    },
    addVectorLayer(map) {
      var iconFeature = new Feature({
        geometry: new Point([0, 0]),
        name: 'Null Island',
        population: 4000,
        rainfall: 500
      })

      var iconStyle = new Style({
        image: new Icon({
          anchor: [0.5, 46],
          anchorXUnits: 'fraction',
          anchorYUnits: 'pixels',
          src: 'https://openlayers.org/en/latest/examples/data/icon.png'
        })
      })

      iconFeature.setStyle(iconStyle)

      var vectorSource = new VectorSource({
        features: [iconFeature]
      })

      var vectorLayer = new VectorLayer({
        source: vectorSource
      })
      map.addLayer(vectorLayer)
    }
  }
}

</script>

<style scoped>
  .map {
    width: 100%;
    height: 100vh;
  }
</style>

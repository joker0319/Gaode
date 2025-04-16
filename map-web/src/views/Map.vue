<script setup>
import { onMounted, ref } from 'vue'
import AMapLoader from '@amap/amap-jsapi-loader'

const map = ref(null)

onMounted(() => {
  initMap()
})

const initMap = async () => {
  try {
    const AMap = await AMapLoader.load({
      key: '02014705b4019e68cd65764c99ad3211',
      version: '2.0',
      plugins: ['AMap.Scale', 'AMap.ToolBar', 'AMap.CircleEditor'],
    })

    map.value = new AMap.Map('container', {
      zoom: 13,
      center: [104.065831, 30.657338],
      viewMode: '2D',
      mapStyle: 'amap://styles/normal',
      layers: [new AMap.TileLayer()],
    })

    map.value.on('complete', () => {
      const circle = new AMap.Circle({
        center: [104.065831, 30.657338],
        radius: 20000,
        strokeColor: '#3366FF',
        strokeWeight: 2,
        strokeOpacity: 0.3,
        fillColor: '#FFA500',
        fillOpacity: 0.1,
      })

      circle.setMap(map.value)
      map.value.setFitView([circle])
    })

    map.value.addControl(new AMap.Scale())
    map.value.addControl(new AMap.ToolBar())

  } catch (error) {
    console.error('地图加载失败：', error)
  }
}
</script>

<template>
  <div class="map-page">
    <div id="container" class="map-container"></div>
  </div>
</template>

<style scoped>
.map-page {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

.map-container {
  width: 100%;
  height: 100%;
  position: absolute;
}
</style> 
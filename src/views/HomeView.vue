<template>
  <!-- 缩放按钮 -->
  <button class="zoomIn" @click="zoomIn">+</button>
  <button class="zoomOut" @click="zoomOut">-</button>

  <!-- 底图 -->
  <div class="map-container" ref="mapContainer">
    <img src="../assets/background.png" class="map-image" ref="mapImage" />

    <!-- 林则徐纪念馆 -->
    <lin_ze_xu_ji_nian_guan :zoom-level="zoomLevel" :top="19" :left="5"></lin_ze_xu_ji_nian_guan>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import lin_ze_xu_ji_nian_guan from '@/components/lin_ze_xu_ji_nian_guan.vue'

const mapImage = ref<HTMLImageElement | null>(null)
const zoomLevel = ref<number>(1)
const zoomStep = 0.2

function zoomIn() {
  zoomLevel.value += zoomStep
  applyZoom()
}

function zoomOut() {
  zoomLevel.value = Math.max(zoomLevel.value - zoomStep, 1)
  applyZoom()
}

function applyZoom() {
  if (mapImage.value) {
    mapImage.value.style.transform = `scale(${zoomLevel.value})`
    mapImage.value.style.transformOrigin = '0 0 0'
  }
}
</script>

<style scoped>

.map-container {
  overflow: scroll;
  height: 100vh;
  width: 100vw;
  position: relative;
}

.map-image {
  height: 100vh;
  width: 100vw;
  transition: transform 0.3s ease;
}

.zoomIn,
.zoomOut {
  cursor: pointer;
  margin-left: 5px;
  border-radius: 25%;
  background-color: white;
  position: absolute;
  width: 50px;
  height: 50px;
  font-size: 30px;
  z-index: 5;
}

.zoomIn {
  top: 10px;
}

.zoomOut {
  top: 70px;
}
</style>

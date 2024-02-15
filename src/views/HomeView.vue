<template>
  <!-- 缩放按钮 -->
  <button class="zoomIn" @click="zoomIn">+</button>
  <button class="zoomOut" @click="zoomOut">-</button>

  <!-- 底图 -->
  <div class="map-container" ref="mapContainer">
    <img src="../assets/background.png" class="map-image" ref="mapImage" />

    <!-- 安泰河 -->
    <An_tai_he :zoom-level="zoomLevel" :top="10" :left="24"></An_tai_he>

    <!-- 三坊七巷名人家风家训馆 -->
    <Ming_ren_jia_feng_jia_xun :zoom-level="zoomLevel" :top="5" :left="35"></Ming_ren_jia_feng_jia_xun>

    <!-- 光禄吟合 -->
    <Guang_lu_yin_he :zoom-level="zoomLevel" :top="23" :left="35"></Guang_lu_yin_he>

    <!-- 林则徐纪念馆 -->
    <lin_ze_xu_ji_nian_guan :zoom-level="zoomLevel" :top="19" :left="5"></lin_ze_xu_ji_nian_guan>
  
     <!-- 瑞来春堂 -->
     <Rui_lai_chun_tang :zoom-level="zoomLevel" :top="27" :left="27"></Rui_lai_chun_tang>

      <!-- 便民资讯点 -->
      <bian_min_zi_xun_dian :zoom-level="zoomLevel" :top="28" :left="31"></bian_min_zi_xun_dian>

      <!-- 至道漆器 -->
      <Zhi_dao_qi_qi :zoom-level="zoomLevel" :top="31" :left="36"></Zhi_dao_qi_qi>

      <!-- 寿山会馆 -->
      <Shou_shan_hui_guan :zoom-level="zoomLevel" :top="34" :left="39"></Shou_shan_hui_guan>

      <!-- 茉莉花茶文化馆 -->
      <Mo_li_hua_cha :zoom-level="zoomLevel" :top="35.5" :left="43.5"></Mo_li_hua_cha>

      <!-- 海上丝绸之路展示馆 -->
      <Hai_shang_si_chou_zhi_lu :zoom-level="zoomLevel" :top="15" :left="43"></Hai_shang_si_chou_zhi_lu>









  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import lin_ze_xu_ji_nian_guan from '@/components/lin_ze_xu_ji_nian_guan.vue'
import An_tai_he from '@/components/an_tai_he.vue';
import Ming_ren_jia_feng_jia_xun from '@/components/ming_ren_jia_feng_jia_xun.vue';
import Guang_lu_yin_he from '@/components/guang_lu_yin_he.vue';
import Rui_lai_chun_tang from '@/components/rui_lai_chun_tang.vue';
import bian_min_zi_xun_dian from '@/components/bian_min_zi_xun_dian.vue';
import Zhi_dao_qi_qi from '@/components/zhi_dao_qi_qi.vue';
import Shou_shan_hui_guan from '@/components/shou_shan_hui_guan.vue';
import Mo_li_hua_cha from '@/components/mo_li_hua_cha.vue';
import Hai_shang_si_chou_zhi_lu from '@/components/hai_shang_si_chou_zhi_lu.vue';

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

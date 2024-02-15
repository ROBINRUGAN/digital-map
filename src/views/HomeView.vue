<template>
  <!-- 缩放按钮 -->
  <button class="zoomIn" @click="zoomIn">➕</button>
  <button class="zoomOut" @click="zoomOut">➖</button>
  <!-- TODO -->
  <button class="aboutUs" @click="zoomOut">❓</button>

  <!-- 底图 -->
  <div class="map-container" ref="mapContainer">
    <img src="../assets/background.png" class="map-image" ref="mapImage" />

    <!-- 安泰河 -->
    <An_tai_he :zoom-level="zoomLevel" :top="10" :left="24"></An_tai_he>

    <!-- 三坊七巷名人家风家训馆 -->
    <Ming_ren_jia_feng_jia_xun
      :zoom-level="zoomLevel"
      :top="5"
      :left="35"
    ></Ming_ren_jia_feng_jia_xun>

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
    <Hai_shang_si_chou_zhi_lu
      :zoom-level="zoomLevel"
      :top="15"
      :left="43"
    ></Hai_shang_si_chou_zhi_lu>

    <!-- 福建海峡民间艺术馆 -->
    <Min_jian_yi_shu_guan :zoom-level="zoomLevel" :top="37" :left="24"></Min_jian_yi_shu_guan>

    <!-- 严复翰墨馆 -->
    <yan_fu_han_mo_guan :zoom-level="zoomLevel" :top="47" :left="24"></yan_fu_han_mo_guan>

    <!-- 三山堂旧址 -->
    <San_shan_tang :zoom-level="zoomLevel" :top="49" :left="32"></San_shan_tang>

    <!-- 鄢家花厅 -->
    <yan_jia_hua_ting :zoom-level="zoomLevel" :top="58" :left="37"></yan_jia_hua_ting>

    <!-- 林聪彝故居 -->
    <Lin_cong_yi_gu_ju :zoom-level="zoomLevel" :top="62" :left="29"></Lin_cong_yi_gu_ju>

    <!-- 勤廉馆 -->
    <Qin_lian_guan :zoom-level="zoomLevel" :top="65" :left="36"></Qin_lian_guan>

    <!-- 坊巷讲习所 -->
    <fang_xiang_jiang_xi_suo :zoom-level="zoomLevel" :top="65" :left="17"></fang_xiang_jiang_xi_suo>

    <!-- 福建华侨主题馆 -->
    <fu_jian_hua_qiao :zoom-level="zoomLevel" :top="74" :left="21"></fu_jian_hua_qiao>

    <!-- 聚春园驿馆 -->
    <ju_chun_yuan_yi_zhan :zoom-level="zoomLevel" :top="71" :left="28"></ju_chun_yuan_yi_zhan>

    <!-- 新四军驻福州办事处旧址 -->
    <Xin_si_jun_zhu_fu_zhou :zoom-level="zoomLevel" :top="73" :left="35"></Xin_si_jun_zhu_fu_zhou>

    <!-- 刘齐街故居 -->
    <liu_qi_jie_gu_ju :zoom-level="zoomLevel" :top="80" :left="25"></liu_qi_jie_gu_ju>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import lin_ze_xu_ji_nian_guan from '@/components/lin_ze_xu_ji_nian_guan.vue'
import An_tai_he from '@/components/an_tai_he.vue'
import Ming_ren_jia_feng_jia_xun from '@/components/ming_ren_jia_feng_jia_xun.vue'
import Guang_lu_yin_he from '@/components/guang_lu_yin_he.vue'
import Rui_lai_chun_tang from '@/components/rui_lai_chun_tang.vue'
import bian_min_zi_xun_dian from '@/components/bian_min_zi_xun_dian.vue'
import Zhi_dao_qi_qi from '@/components/zhi_dao_qi_qi.vue'
import Shou_shan_hui_guan from '@/components/shou_shan_hui_guan.vue'
import Mo_li_hua_cha from '@/components/mo_li_hua_cha.vue'
import Hai_shang_si_chou_zhi_lu from '@/components/hai_shang_si_chou_zhi_lu.vue'
import Min_jian_yi_shu_guan from '@/components/min_jian_yi_shu_guan.vue'
import yan_fu_han_mo_guan from '@/components/yan_fu_han_mo_guan.vue'
import San_shan_tang from '@/components/san_shan_tang.vue'
import yan_jia_hua_ting from '@/components/yan_jia_hua_ting.vue'
import Lin_cong_yi_gu_ju from '@/components/lin_cong_yi_gu_ju.vue'
import Qin_lian_guan from '@/components/qin_lian_guan.vue'
import fang_xiang_jiang_xi_suo from '@/components/fang_xiang_jiang_xi_suo.vue'
import fu_jian_hua_qiao from '@/components/fu_jian_hua_qiao.vue'
import ju_chun_yuan_yi_zhan from '@/components/ju_chun_yuan_yi_zhan.vue'
import Xin_si_jun_zhu_fu_zhou from '@/components/xin_si_jun_zhu_fu_zhou.vue'
import liu_qi_jie_gu_ju from '@/components/liu_qi_jie_gu_ju.vue'

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
.zoomOut,
.aboutUs {
  cursor: pointer;
  margin-left: 5px;
  border-radius: 25%;
  background-color: rgb(255, 255, 255, 0.8);
  position: absolute;
  transition: all 0.1s ease-in-out;
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

.aboutUs {
  top: 130px;
}

.zoomIn:hover,
.zoomOut:hover,
.aboutUs:hover {
  background-color: rgb(255, 255, 255, 1);
}
</style>

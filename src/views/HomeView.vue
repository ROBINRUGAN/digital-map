<template>
  <!-- 缩放按钮 -->
  <button class="zoomIn" @click="zoomIn">➕</button>
  <button class="zoomOut" @click="zoomOut">➖</button>

  <!-- Github -->
  <button class="github" @click="gotoGithub">
    <i class="bi bi-github"></i>
  </button>

  <!-- 帮助 -->
  <el-popover placement="right" :width="445" trigger="hover">
    <template #reference>
      <button class="aboutUs" @click="zoomOut">❓</button>
    </template>
    <div class="aboutInfo">
      <h3>关于我们</h3>
      <p>
        这是福州大学计算机与大数据学院2024寒假三下乡“古厝新数，行迹福州”数字地图，基于Vue3+TypeScript开发。详情可点击上方按钮进入GitHub仓库页查看。
      </p>
      <p>技术组成员：吴荣榜，梅明胜</p>
      <br />
      <p>
        点击地图上的标记点📌，可以查看相关景点的图片和文字介绍📝，再次点击图片可查看高清大图🏞️。
      </p>
      <p>点击左侧的放大按钮➕和缩小按钮➖，可以放大或缩小地图。</p>
    </div>
  </el-popover>

  <InfoDetail :id="exactId" ref="OpenHook" />

  <!-- 底图 -->
  <div class="map-container" ref="mapContainer">
    <img src="../assets/background.png" @load="onImageLoaded" class="map-image" ref="mapImage" />

    <!-- 安泰河 -->
    <An_tai_he :zoom-level="zoomLevel" :top="10" :left="24" @click="showDetail(3)"></An_tai_he>

    <!-- 三坊七巷名人家风家训馆 -->
    <Ming_ren_jia_feng_jia_xun
      :zoom-level="zoomLevel"
      :top="5"
      :left="35"
      @click="showDetail(4)"
    ></Ming_ren_jia_feng_jia_xun>

    <!-- 光禄吟合 -->
    <Guang_lu_yin_he
      :zoom-level="zoomLevel"
      :top="23"
      :left="35"
      @click="showDetail(5)"
    ></Guang_lu_yin_he>

    <!-- 林则徐纪念馆 -->
    <Lin_ze_xu_ji_nian_guan
      :zoom-level="zoomLevel"
      :top="19"
      :left="5"
      @click="showDetail(1)"
    ></Lin_ze_xu_ji_nian_guan>

    <!-- 瑞来春堂 -->
    <Rui_lai_chun_tang
      :zoom-level="zoomLevel"
      :top="27"
      :left="27"
      @click="showDetail(6)"
    ></Rui_lai_chun_tang>

    <!-- 美术馆 -->
    <Mei_shu_guan
      :zoom-level="zoomLevel"
      :top="28"
      :left="31"
      @click="showDetail(7)"
    ></Mei_shu_guan>

    <!-- 至道漆器 -->
    <Zhi_dao_qi_qi
      :zoom-level="zoomLevel"
      :top="31"
      :left="36"
      @click="showDetail(8)"
    ></Zhi_dao_qi_qi>

    <!-- 寿山会馆 -->
    <Shou_shan_hui_guan
      :zoom-level="zoomLevel"
      :top="34"
      :left="39"
      @click="showDetail(9)"
    ></Shou_shan_hui_guan>

    <!-- 茉莉花茶文化馆 -->
    <Mo_li_hua_cha
      :zoom-level="zoomLevel"
      :top="35.5"
      :left="43.5"
      @click="showDetail(10)"
    ></Mo_li_hua_cha>

    <!-- 海上丝绸之路展示馆 -->
    <Hai_shang_si_chou_zhi_lu
      :zoom-level="zoomLevel"
      :top="15"
      :left="43"
      @click="showDetail(11)"
    ></Hai_shang_si_chou_zhi_lu>

    <!-- 福建海峡民间艺术馆 -->
    <Min_jian_yi_shu_guan
      :zoom-level="zoomLevel"
      :top="37"
      :left="24"
      @click="showDetail(12)"
    ></Min_jian_yi_shu_guan>

    <!-- 严复翰墨馆 -->
    <Yan_fu_han_mo_guan
      :zoom-level="zoomLevel"
      :top="47"
      :left="24"
      @click="showDetail(13)"
    ></Yan_fu_han_mo_guan>

    <!-- 三山堂旧址 -->
    <San_shan_tang
      :zoom-level="zoomLevel"
      :top="49"
      :left="32"
      @click="showDetail(14)"
    ></San_shan_tang>

    <!-- 鄢家花厅 -->
    <Yan_jia_hua_ting
      :zoom-level="zoomLevel"
      :top="58"
      :left="37"
      @click="showDetail(15)"
    ></Yan_jia_hua_ting>

    <!-- 林聪彝故居 -->
    <Lin_cong_yi_gu_ju
      :zoom-level="zoomLevel"
      :top="62"
      :left="29"
      @click="showDetail(16)"
    ></Lin_cong_yi_gu_ju>

    <!-- 勤廉馆 -->
    <Qin_lian_guan
      :zoom-level="zoomLevel"
      :top="65"
      :left="36"
      @click="showDetail(17)"
    ></Qin_lian_guan>

    <!-- 坊巷讲习所 -->
    <Fang_xiang_jiang_xi_suo
      :zoom-level="zoomLevel"
      :top="65"
      :left="17"
      @click="showDetail(2)"
    ></Fang_xiang_jiang_xi_suo>

    <!-- 福建华侨主题馆 -->
    <Fu_jian_hua_qiao
      :zoom-level="zoomLevel"
      :top="74"
      :left="21"
      @click="showDetail(18)"
    ></Fu_jian_hua_qiao>

    <!-- 聚春园驿馆 -->
    <Ju_chun_yuan_yi_zhan
      :zoom-level="zoomLevel"
      :top="71"
      :left="28"
      @click="showDetail(19)"
    ></Ju_chun_yuan_yi_zhan>

    <!-- 新四军驻福州办事处旧址 -->
    <Xin_si_jun_zhu_fu_zhou
      :zoom-level="zoomLevel"
      :top="73"
      :left="35"
      @click="showDetail(20)"
    ></Xin_si_jun_zhu_fu_zhou>

    <!-- 刘齐街故居 -->
    <Liu_qi_jie_gu_ju
      :zoom-level="zoomLevel"
      :top="80"
      :left="25"
      @click="showDetail(21)"
    ></Liu_qi_jie_gu_ju>

    <!-- 古厝福礼 -->
    <Gu_cuo_fu_li
      :zoom-level="zoomLevel"
      :top="42"
      :left="44"
      @click="showDetail(22)"
    ></Gu_cuo_fu_li>

    <!-- 福小邮的家 -->
    <Fu_xiao_you :zoom-level="zoomLevel" :top="43" :left="48" @click="showDetail(23)"></Fu_xiao_you>

    <!-- 南后街展览馆 -->
    <Nan_hou_jie
      :zoom-level="zoomLevel"
      :top="44"
      :left="52.5"
      @click="showDetail(24)"
    ></Nan_hou_jie>

    <!-- 中瑞影城 -->
    <Zhong_rui_ying_cheng
      :zoom-level="zoomLevel"
      :top="51"
      :left="47"
      @click="showDetail(25)"
    ></Zhong_rui_ying_cheng>

    <!-- 安民半舍 -->
    <An_min_ban_she
      :zoom-level="zoomLevel"
      :top="64"
      :left="42.5"
      @click="showDetail(26)"
    ></An_min_ban_she>

    <!-- 唯美客 -->
    <Wei_mei_ke :zoom-level="zoomLevel" :top="69" :left="50" @click="showDetail(27)"></Wei_mei_ke>

    <!-- 中共福州市委旧址 -->
    <Zhong_gong_fu_zhou_shi_wei
      :zoom-level="zoomLevel"
      :top="72"
      :left="42"
      @click="showDetail(28)"
    ></Zhong_gong_fu_zhou_shi_wei>

    <!-- 台湾会馆 -->
    <Tai_wan_hui_guan
      :zoom-level="zoomLevel"
      :top="61.5"
      :left="54"
      @click="showDetail(29)"
    ></Tai_wan_hui_guan>

    <!-- 小黄楼 -->
    <Xiao_huang_lou
      :zoom-level="zoomLevel"
      :top="61"
      :left="59"
      @click="showDetail(30)"
    ></Xiao_huang_lou>

    <!-- 秦隐 安珀 -->
    <Qin_yin_an_bo
      :zoom-level="zoomLevel"
      :top="68"
      :left="57"
      @click="showDetail(31)"
    ></Qin_yin_an_bo>

    <!-- 宜美术馆 -->
    <Yi_mei_shu_guan
      :zoom-level="zoomLevel"
      :top="79"
      :left="53"
      @click="showDetail(32)"
    ></Yi_mei_shu_guan>

    <!-- 郭柏荫故居 -->
    <Guo_bai_yin_gu_ju
      :zoom-level="zoomLevel"
      :top="85"
      :left="51.5"
      @click="showDetail(33)"
    ></Guo_bai_yin_gu_ju>

    <!-- 美喜悦舍 -->
    <Mei_xi_yue_she
      :zoom-level="zoomLevel"
      :top="84"
      :left="65"
      @click="showDetail(34)"
    ></Mei_xi_yue_she>

    <!-- 永和鱼丸 -->
    <Yong_he_yu_wan
      :zoom-level="zoomLevel"
      :top="50"
      :left="70"
      @click="showDetail(35)"
    ></Yong_he_yu_wan>

    <!-- 商印馆 -->
    <Shang_yin_guan
      :zoom-level="zoomLevel"
      :top="19"
      :left="52"
      @click="showDetail(36)"
    ></Shang_yin_guan>

    <!-- 乡约碑 -->
    <Xiang_yue_bei
      :zoom-level="zoomLevel"
      :top="27"
      :left="49"
      @click="showDetail(37)"
    ></Xiang_yue_bei>

    <!-- 福建省非物质文化遗产博览苑 -->
    <Fei_wu_zhi_wen_hua
      :zoom-level="zoomLevel"
      :top="33"
      :left="52"
      @click="showDetail(38)"
    ></Fei_wu_zhi_wen_hua>

    <!-- 欧阳花厅 -->
    <Ou_yang_hua_ting
      :zoom-level="zoomLevel"
      :top="6"
      :left="70"
      @click="showDetail(39)"
    ></Ou_yang_hua_ting>

    <!-- 水榭戏台 -->
    <Shui_xie_xi_tai
      :zoom-level="zoomLevel"
      :top="20"
      :left="72"
      @click="showDetail(40)"
    ></Shui_xie_xi_tai>

    <!-- 同利肉燕 -->
    <Tong_li_rou_yan
      :zoom-level="zoomLevel"
      :top="37"
      :left="65"
      @click="showDetail(41)"
    ></Tong_li_rou_yan>

    <!-- 林觉民冰心故居 -->
    <Lin_jue_min_bing_xin
      :zoom-level="zoomLevel"
      :top="27"
      :left="94.2"
      @click="showDetail(42)"
    ></Lin_jue_min_bing_xin>

    <!-- 风雨廊 -->
    <Feng_yu_lang
      :zoom-level="zoomLevel"
      :top="47"
      :left="85"
      @click="showDetail(43)"
    ></Feng_yu_lang>

    <!-- 星巴克咖啡 -->
    <Xing_ba_ke_ka_fei
      :zoom-level="zoomLevel"
      :top="52"
      :left="80"
      @click="showDetail(44)"
    ></Xing_ba_ke_ka_fei>

    <!-- 王麒故居 -->
    <Wang_qi_gu_ju
      :zoom-level="zoomLevel"
      :top="58"
      :left="77"
      @click="showDetail(45)"
    ></Wang_qi_gu_ju>

    <!-- 福建民俗博物馆 -->
    <Min_su_bo_wu_guan
      :zoom-level="zoomLevel"
      :top="62"
      :left="80"
      @click="showDetail(46)"
    ></Min_su_bo_wu_guan>

    <!-- 畲族馆 -->
    <She_zu_guan :zoom-level="zoomLevel" :top="60" :left="87" @click="showDetail(47)"></She_zu_guan>

    <!-- 天后宫 -->
    <Tian_hou_gong
      :zoom-level="zoomLevel"
      :top="71"
      :left="78"
      @click="showDetail(48)"
    ></Tian_hou_gong>

    <!-- 严复故居 -->
    <Yan_fu_gu_ju
      :zoom-level="zoomLevel"
      :top="73"
      :left="85"
      @click="showDetail(49)"
    ></Yan_fu_gu_ju>

    <!-- 绥安会馆 -->
    <Sui_an_hui_guan
      :zoom-level="zoomLevel"
      :top="78"
      :left="77"
      @click="showDetail(50)"
    ></Sui_an_hui_guan>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { ElLoading } from 'element-plus'
import Lin_ze_xu_ji_nian_guan from '@/components/location/lin_ze_xu_ji_nian_guan.vue'
import An_tai_he from '@/components/location/an_tai_he.vue'
import Ming_ren_jia_feng_jia_xun from '@/components/location/ming_ren_jia_feng_jia_xun.vue'
import Guang_lu_yin_he from '@/components/location/guang_lu_yin_he.vue'
import Rui_lai_chun_tang from '@/components/location/rui_lai_chun_tang.vue'
import Mei_shu_guan from '@/components/location/mei_shu_guan.vue'
import Zhi_dao_qi_qi from '@/components/location/zhi_dao_qi_qi.vue'
import Shou_shan_hui_guan from '@/components/location/shou_shan_hui_guan.vue'
import Mo_li_hua_cha from '@/components/location/mo_li_hua_cha.vue'
import Hai_shang_si_chou_zhi_lu from '@/components/location/hai_shang_si_chou_zhi_lu.vue'
import Min_jian_yi_shu_guan from '@/components/location/min_jian_yi_shu_guan.vue'
import Yan_fu_han_mo_guan from '@/components/location/yan_fu_han_mo_guan.vue'
import San_shan_tang from '@/components/location/san_shan_tang.vue'
import Yan_jia_hua_ting from '@/components/location/yan_jia_hua_ting.vue'
import Lin_cong_yi_gu_ju from '@/components/location/lin_cong_yi_gu_ju.vue'
import Qin_lian_guan from '@/components/location/qin_lian_guan.vue'
import Fang_xiang_jiang_xi_suo from '@/components/location/fang_xiang_jiang_xi_suo.vue'
import Fu_jian_hua_qiao from '@/components/location/fu_jian_hua_qiao.vue'
import Ju_chun_yuan_yi_zhan from '@/components/location/ju_chun_yuan_yi_zhan.vue'
import Xin_si_jun_zhu_fu_zhou from '@/components/location/xin_si_jun_zhu_fu_zhou.vue'
import Liu_qi_jie_gu_ju from '@/components/location/liu_qi_jie_gu_ju.vue'
import Gu_cuo_fu_li from '@/components/location/gu_cuo_fu_li.vue'
import Fu_xiao_you from '@/components/location/fu_xiao_you.vue'
import Nan_hou_jie from '@/components/location/nan_hou_jie.vue'
import Zhong_rui_ying_cheng from '@/components/location/zhong_rui_ying_cheng.vue'
import An_min_ban_she from '@/components/location/an_min_ban_she.vue'
import Wei_mei_ke from '@/components/location/wei_mei_ke.vue'
import Zhong_gong_fu_zhou_shi_wei from '@/components/location/zhong_gong_fu_zhou_shi_wei.vue'
import Tai_wan_hui_guan from '@/components/location/tai_wan_hui_guan.vue'
import Xiao_huang_lou from '@/components/location/xiao_huang_lou.vue'
import Qin_yin_an_bo from '@/components/location/qin_yin_an_bo.vue'
import Yi_mei_shu_guan from '@/components/location/yi_mei_shu_guan.vue'
import Guo_bai_yin_gu_ju from '@/components/location/guo_bai_yin_gu_ju.vue'
import Mei_xi_yue_she from '@/components/location/mei_xi_yue_she.vue'
import Yong_he_yu_wan from '@/components/location/yong_he_yu_wan.vue'
import Shang_yin_guan from '@/components/location/shang_yin_guan.vue'
import Xiang_yue_bei from '@/components/location/xiang_yue_bei.vue'
import Fei_wu_zhi_wen_hua from '@/components/location/fei_wu_zhi_wen_hua.vue'
import Ou_yang_hua_ting from '@/components/location/ou_yang_hua_ting.vue'
import Shui_xie_xi_tai from '@/components/location/shui_xie_xi_tai.vue'
import Tong_li_rou_yan from '@/components/location/tong_li_rou_yan.vue'
import Lin_jue_min_bing_xin from '@/components/location/lin_jue_min_bing_xin.vue'
import Feng_yu_lang from '@/components/location/feng_yu_lang.vue'
import Xing_ba_ke_ka_fei from '@/components/location/xing_ba_ke_ka_fei.vue'
import Wang_qi_gu_ju from '@/components/location/wang_qi_gu_ju.vue'
import Min_su_bo_wu_guan from '@/components/location/min_su_bo_wu_guan.vue'
import She_zu_guan from '@/components/location/she_zu_guan.vue'
import Tian_hou_gong from '@/components/location/tian_hou_gong.vue'
import Yan_fu_gu_ju from '@/components/location/yan_fu_gu_ju.vue'
import Sui_an_hui_guan from '@/components/location/sui_an_hui_guan.vue'
import InfoDetail from '@/components/InfoDetail.vue'

const mapImage = ref<HTMLImageElement | null>(null)
const zoomLevel = ref<number>(1)
const exactId = ref<number>(0)
const zoomStep = 0.1
const OpenHook = ref<typeof InfoDetail | null>(null)
let loadingInstance: { close: () => void } | null = null

// 跳转到仓库地址https://github.com/ROBINRUGAN/digital-map
const gotoGithub = () => {
  window.location.href = 'https://github.com/ROBINRUGAN/digital-map'
}

onMounted(() => {
  loadingInstance = ElLoading.service({
    lock: true,
    text: '加载中...',
    background: 'rgba(255, 255, 255, 0.7)'
  })
})
function showDetail(id: number) {
  exactId.value = id
  OpenHook.value!.loadScenicSpotInfo(id)
}

function onImageLoaded() {
  if (loadingInstance) {
    setTimeout(() => {
      loadingInstance!.close() // 关闭加载蒙版
    }, 2000)
  }
}

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

<style>
.el-popper {
  padding: 0 !important;
  background-color: transparent !important;
  border-color: transparent !important;
  box-shadow: 0 0 10px 0px rgba(0, 0, 0, 1) !important;
  border-radius: 20px !important;
}
.el-popper.is-light .el-popper__arrow::before {
  background: #c9c5c5d8 !important;
  box-shadow: 0 0 10px 0 rgba(0, 0, 0, 1) !important;
  border-color: transparent !important;
}
</style>
<style scoped>
.aboutInfo {
  background-color: #c9c5c5d8;
  padding: 18px;
  font-size: 20px;
  border-radius: 20px;
  color: rgb(53, 52, 52);
  line-height: 25px;
}
h3 {
  font-size: 24px;
  margin-top: 5px;
  margin-bottom: 10px;
  text-align: center;
  color: rgb(171, 27, 27);
  text-indent: 0;
}

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
/* 手机端展示 */
@media screen and (max-width: 768px) {
  .map-image {
    height: 717px;
    width: 1350px;
    transition: transform 0.3s ease;
  }
  .map-container {
    overflow: auto;
    height: 717px;
    width: 1350px;
    position: relative;
  }
}

.zoomIn,
.zoomOut,
.aboutUs,
.github {
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
  top: 190px;
}
.github {
  top: 130px;
}

.zoomIn:hover,
.zoomOut:hover,
.aboutUs:hover,
.github:hover {
  background-color: rgb(255, 255, 255, 1);
}
</style>

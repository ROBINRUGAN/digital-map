<template>
  <el-button plain @click="dialogTableVisible = true"> 你好 </el-button>

  <el-dialog v-model="dialogTableVisible" class="dialog" title="林则徐纪念馆" width="1000">
    <!-- 轮播图展示图片 -->
    <el-carousel height="190px" >
      <el-carousel-item>
        <img src="../assets/test.jpg">
      </el-carousel-item>
      <el-carousel-item>
        <img src="../assets/test1.jpg">
      </el-carousel-item>
    </el-carousel>
    <!-- 文字介绍 -->
    <div class="text-center">
      <p>
        林则徐纪念馆位于福建省福州市鼓楼区，是为纪念清代福建巡抚林则徐而建的纪念馆。林则徐是中国近代史上的一位杰出的政治家、军事家、外交家、教育家、文学家
        林则徐纪念馆位于福建省福州市鼓楼区，是为纪念清代福建巡抚林则徐而建的纪念馆。林则徐是中国近代史上的一位杰出的政治家、军事家、外交家、教育家、文学家
        林则徐纪念馆位于福建省福州市鼓楼区，是为纪念清代福建巡抚林则徐而建的纪念馆。林则徐是中国近代史上的一位杰出的政治家、军事家、外交家、教育家、文学家
        林则徐纪念馆位于福建省福州市鼓楼区，是为纪念清代福建巡
      </p>
    </div>

  </el-dialog>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

const dialogTableVisible = ref(true)

</script>

<style>
.el-dialog{
  background-image: url('@/assets/dialog_background.png') !important;
  background-size: contain !important;
  height: 530px !important;
  border: none !important;
  width: 507px !important;
  background-color: transparent !important;
}
.el-carousel{
    width: 390px;
    margin-left: 5px;
    border-radius: 20px;
}
.el-dialog__title{
  font-size: 22px !important;
  margin-left: 12px !important;
  color: #981717;
}
</style>

<style scoped>
img{
  width: 100%;
  object-fit:cover;
}
.text-center {
  border-radius: 10px;
  margin: auto;
  width: 94%;
  font-size: 16px;
  color: rgb(59, 58, 58);
  line-height: 20px;
  overflow: scroll;
  height: 140px;
  padding: 5px;
  border-style:dashed;
  border-color: #8D5E55;
  margin-top: 15px;
}

.demonstration {
  color: var(--el-text-color-secondary);
}

.el-carousel__item h3 {
  color: #475669;
  opacity: 0.75;
  line-height: 150px;
  margin: 0;
  text-align: center;
}

.el-carousel__item:nth-child(2n) {
  background-color: #99a9bf;
}

.el-carousel__item:nth-child(2n + 1) {
  background-color: #d3dce6;
}

</style>

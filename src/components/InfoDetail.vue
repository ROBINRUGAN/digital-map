<template>
  <el-dialog v-model="dialogTableVisible" class="dialog" :title="title" width="1000">
    <!-- 轮播图展示图片 -->
    <el-carousel height="190px">
      <el-carousel-item v-for="(image, index) in images" :key="index">
        <img :src="image" />
      </el-carousel-item>
    </el-carousel>

    <!-- 文字介绍 -->
    <div class="text-center">
      <p>
        {{ description }}
      </p>
    </div>
  </el-dialog>
</template>

<script lang="ts" setup>
import { ElMessage } from 'element-plus';
import { ref, defineExpose } from 'vue'

const dialogTableVisible = ref(false)
const title = ref('')
const description = ref('')
const images = ref([])
const same = ref(true)
interface SpotInfo {
  id: number
  title: string
  description: string
  images: string[]
}

const loadScenicSpotInfo = async (id: number) => {
    same.value = false
    const response = await fetch('/data/spots.json') // 确保路径正确
    const { spots } = await response.json()
    const spot = spots.find((s: SpotInfo) => s.id === id)
    if (spot) {
      title.value = spot.title
      description.value = spot.description
      images.value = spot.images
      dialogTableVisible.value = true
    } else {
      dialogTableVisible.value = false
      ElMessage.error('该景点信息待完善')
    }
}

defineExpose({ loadScenicSpotInfo, same })
</script>

<style>
.el-dialog {
  background-image: url('@/assets/dialog_background.png') !important;
  background-size: contain !important;
  height: 530px !important;
  border: none !important;
  width: 507px !important;
  background-color: transparent !important;
}
.el-carousel {
  width: 390px;
  margin-left: 5px;
  border-radius: 20px;
}
.el-dialog__title {
  font-size: 22px !important;
  margin-left: 12px !important;
  color: #981717;
}
</style>

<style scoped>
img {
  width: 100%;
  object-fit: cover;
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
  border-style: dashed;
  border-color: #8d5e55;
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

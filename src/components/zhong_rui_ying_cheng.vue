<template>
  <button
    class="map-point"
    :style="pointStyle"
    @mouseenter="hovering = true"
    @mouseleave="hovering = false"
  ></button>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

const props = defineProps({
  zoomLevel: Number,
  top: Number,
  left: Number
})

const hovering = ref(false) // 用于追踪鼠标是否悬停在元素上

// 根据鼠标悬停状态动态计算标记点的样式
const pointStyle = computed(() => {
  const scale = hovering.value ? 1.07 * props.zoomLevel! : props.zoomLevel // 当鼠标悬停时增加缩放比例
  return {
    transform: `scale(${scale})`,
    transformOrigin: `${hovering.value ? 0.5 : 0} ${hovering.value ? 0.5 : 0} 0`,
    top: `${props.top! * props.zoomLevel!}%`,
    left: `${props.left! * props.zoomLevel!}%`
  }
})
</script>

<style scoped>
.map-point {
  width: 90px;
  height: 45px;
  background-size: 100%;
  cursor: pointer;
  background-color: transparent;
  border: none;
  background-image: url('../assets/zhong_rui_ying_cheng.png');
  position: absolute;
  transition: all 0.3s ease;
  z-index: 4;
}
</style>

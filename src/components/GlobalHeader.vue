<template>
  <div id="global-header" class="header-area" v-show="visible" :class="{ solid: solid }">
    <div class="overlay" v-show="showOverlay"></div>
    <nav class="site-menu">
      <a href="/" @mouseenter="showOverlay = true" @mouseleave="showOverlay = false">首页</a>
      <a href="/learning" @mouseenter="showOverlay = true" @mouseleave="showOverlay = false"
        >学习</a
      >
      <a href="/blog" @mouseenter="showOverlay = true" @mouseleave="showOverlay = false">随笔</a>
      <a href="/portfolio" @mouseenter="showOverlay = true" @mouseleave="showOverlay = false"
        >作品集</a
      >
      <a href="/about" @mouseenter="showOverlay = true" @mouseleave="showOverlay = false">关于</a>
    </nav>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const { visible } = defineProps<{
  visible: boolean
  solid: boolean
}>()

const showOverlay = ref(false)
</script>

<style scoped>
.header-area {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background-color: transparent;
  z-index: 1000;
  transition: background-color 0.3s ease;
}

.header-area.solid {
  background-color: rgba(0, 0, 0, 0.4);
  backdrop-filter: blur(6px);
  border-bottom-left-radius: 12px;
  border-bottom-right-radius: 12px;
  transition:
    background-color 0.3s ease,
    border-radius 0.3s ease;
}

.header-area[style*='display: none'] {
  opacity: 0;
}

.site-menu {
  display: flex;
  justify-content: center; /* 居中 */
  gap: 16px;
  position: relative;
  z-index: 1001;
}

.site-menu a {
  color: white;
  text-decoration: none;
  font-weight: 500;
  font-size: 16px;
  padding: 13px 12px;
  border-radius: 6px;
  position: relative;
  transition: color 0.3s ease;
}

.site-menu a:hover {
  color: #38bdf8;
}

.site-menu a:hover::after {
  width: 100%;
}

/* 蒙层样式 */
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: linear-gradient(to bottom, rgba(255, 255, 255, 0.6), rgba(255, 255, 255, 0));
  backdrop-filter: blur(10px);
  z-index: 999;
  transition: opacity 0.3s ease;
  pointer-events: none; /* ⚠️ 不干扰鼠标点击 */
}

/* 上滑导航样式 */
</style>

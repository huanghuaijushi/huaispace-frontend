<template>
  <div class="app-wrapper">
    <GlobalHeader :visible="showHeader" :solid="solidHeader" />
    <HomeView />
  </div>
</template>

<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue'
import HomeView from './views/HomeView.vue'
import GlobalHeader from '@/components/GlobalHeader.vue'

const showHeader = ref(true)
const solidHeader = ref(false)
let lastScrollY = window.scrollY

// const onScroll = () => {
//   const currentScrollY = window.scrollY
//   const hero = document.querySelector('.hero')

//   if (hero) {
//     const rect = hero.getBoundingClientRect()
//     // 如果 Hero 还在屏幕里 → 显示导航、透明
//     if (rect.bottom > 0) {
//       showHeader.value = true
//       solidHeader.value = false
//     } else {
//       // Hero 离开了，就看滚动方向
//       if (currentScrollY > lastScrollY) {
//         // 向下滑 → 隐藏导航
//         showHeader.value = false
//       } else {
//         // 向上滑 → 显示 + 固定导航栏
//         showHeader.value = true
//         solidHeader.value = true
//       }
//     }
//   }

//   lastScrollY = currentScrollY // 更新为最新位置
// }
const onScroll = () => {
  const currentScrollY = window.scrollY
  const hero = document.querySelector('.hero')

  // 如果回到最顶部，就显示透明导航
  if (currentScrollY === 0) {
    showHeader.value = true
    solidHeader.value = false
  } else if (hero) {
    const rect = hero.getBoundingClientRect()

    // 如果 hero 已经离开视口
    if (rect.bottom <= 0) {
      if (currentScrollY > lastScrollY) {
        // 向下滚动：隐藏导航
        showHeader.value = false
      } else {
        // 向上滚动：显示 + 背景导航
        showHeader.value = true
        solidHeader.value = true
      }
    }
  }

  lastScrollY = currentScrollY
}

onMounted(() => {
  window.addEventListener('scroll', onScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', onScroll)
})
</script>

<style>
body {
  margin: 0;
}

.app-wrapper {
  position: relative;
  width: 100%;
  height: 100%;
  overflow-x: hidden;
}
</style>

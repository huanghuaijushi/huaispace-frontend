<template>
  <div class="home">
    <section class="hero"></section>
    <main class="main-content">
      <h2>这里是首页内容</h2>
      <p>继续向下滚动，你就看不到顶部背景图了。</p>
    </main>
  </div>
</template>

<script setup lang="ts"></script>

<style scoped>
.hero {
  background-image: url('@/assets/images/bg.png');
  background-size: cover;
  background-position: center;
  height: 100vh;
  display: flex;
  align-items: flex-start;
  color: white;
}

.main-content {
  padding: 40px;
  height: 100vh;
}
</style>

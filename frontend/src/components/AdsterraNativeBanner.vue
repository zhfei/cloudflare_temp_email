<template>
  <div class="ad-native-wrapper">
    <!-- 
      使用真实 src 而不是 srcdoc，解决 403 Forbidden (Referer 限制)问题，
      同时也隔离了 SPA 运行时环境，保证路由切换时脚本能重复执行。
    -->
    <iframe
      src="/adsterra-native.html"
      frameborder="0"
      scrolling="no"
      width="100%"
      height="140"
      style="border: none; overflow: hidden; background: transparent;"
    ></iframe>
  </div>
</template>

<script setup>
</script>

<style scoped>
.ad-native-wrapper {
  width: 100%;
  margin: 16px 0;
  display: flex;
  justify-content: center;
  min-height: 140px;
}
</style>

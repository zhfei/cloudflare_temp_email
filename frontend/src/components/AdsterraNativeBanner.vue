<script setup>
import { onMounted, ref } from 'vue'

const container = ref(null)

onMounted(() => {
  if (!container.value) return

  // 防止重复加载
  const scriptId = 'adsterra-native-banner-script'
  if (!document.getElementById(scriptId)) {
    const script = document.createElement('script')
    script.id = scriptId
    script.async = true
    script.setAttribute('data-cfasync', 'false')
    script.src = 'https://pl28857670.effectivegatecpm.com/a1c9548452fc07cd7761086d0e555924/invoke.js'
    document.head.appendChild(script)
  }
})
</script>

<template>
  <div class="ad-native-wrapper" ref="container">
    <div id="container-a1c9548452fc07cd7761086d0e555924"></div>
  </div>
</template>

<style scoped>
.ad-native-wrapper {
  width: 100%;
  margin: 12px 0;
  min-height: 60px;
}
</style>

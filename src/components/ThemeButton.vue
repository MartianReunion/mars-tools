<template>
  <button @click="toggleTheme">
    <Sun :size="16" color="var(--svg-stroke-color)"/>
  </button>
</template>

<script setup lang="ts">
import {ref, onMounted, watch} from 'vue'
import {Sun} from "lucide-vue-next";

const currentTheme = ref('light') // 默认主题

// 切换主题
const toggleTheme = () => {
  const newTheme = currentTheme.value === 'dark' ? 'light' : 'dark'
  currentTheme.value = newTheme
  applyTheme(newTheme)
}

// 应用主题
const applyTheme = (theme: string) => {
  // 移除旧的主题link
  const oldLink = document.getElementById('theme-style')
  if (oldLink) {
    oldLink.remove()
  }

  // 创建新的link标签
  const link = document.createElement('link')
  link.id = 'theme-style'
  link.rel = 'stylesheet'
  link.href = `/themes/${theme}.css` // 或直接写路径：`./${theme}.css`

  document.head.appendChild(link)
}

// 初始化主题（从localStorage读取）
onMounted(() => {
  const savedTheme = localStorage.getItem('theme') || 'dark'
  currentTheme.value = savedTheme
  applyTheme(savedTheme)
})

// 监听主题变化，保存到localStorage
watch(currentTheme, (newTheme) => {
  localStorage.setItem('theme', newTheme)
})
</script>
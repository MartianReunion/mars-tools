<script setup lang="ts">

import {X, Minus, Diamond} from 'lucide-vue-next'

import {Window} from '@tauri-apps/api/window';
import ThemeButton from "./ThemeButton.vue";

const appWindow = new Window('main');

function minimizeWindow(): void {
  appWindow.minimize();
}

function toggleMaximizeWindow(): void {
  appWindow.toggleMaximize();
}

function closeWindow(): void {
  appWindow.close()
}

</script>

<template>
  <header data-tauri-drag-region class="header">
    <div class="header-left">
      <img src="/icon.png" alt="图标" class="logo-icon">
      <ThemeButton/>
    </div>

    <div class="header-center" data-tauri-drag-region>
      <p class="window-title">火星工具箱</p>
    </div>

    <div class="header-right">
      <button class="btn">
        <Minus :size="16" color="var(--svg-stroke-color)" @click="minimizeWindow()"/>
      </button>
      <button class="btn">
        <Diamond :size="16" color="var(--svg-stroke-color)" @click="toggleMaximizeWindow()"/>
      </button>
      <button class="btn">
        <X :size="16" color="var(--svg-stroke-color)" @click="closeWindow()"/>
      </button>
    </div>
  </header>
</template>

<style scoped>
/* 求闻百科 Header 样式 */
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: var(--title-bar-color);
  padding: 0 16px;
  border-bottom: 1px solid var(--border-color);
  height: 40px;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  user-select: none;
  transition: background-color 0.2s ease;
}

.header-left {
  display: flex;
  align-items: center;
  gap: 5px;
  flex-shrink: 0; /* 防止右侧区域被压缩 */
  transition: background-color 0.2s ease;
}

.header-center {
  position: absolute; /* 绝对定位实现完美居中 */
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  align-items: center;
  height: 100%;
  transition: background-color 0.2s ease;
}

.header-right {
  display: flex;
  align-items: center;
  gap: 5px;
  flex-shrink: 0; /* 防止右侧区域被压缩 */
  transition: color 0.2s ease, background-color 0.2s ease
}

.logo-icon {
  width: 24px;
  height: 24px;
  padding-right: 16px;
  border-right: 1px solid var(--border-color);
  margin-right: 10px;
  transition: background-color 0.2s ease;
}

button {
  background: none;
  border: none;
  cursor: pointer;
  padding: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 4px;
  transition: background-color 0.2s ease;
}

button:hover {
  background-color: var(--btn-cover-color);
}
</style>
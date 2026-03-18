<script setup lang="ts">
import TitleBar from "./components/TitleBar.vue";
import Sidebar from "./components/Sidebar.vue";
import { ref, computed } from 'vue'           // ✅ 运行时 API
import type { Component } from 'vue'          // ✅ 类型单独导入
import HomePage from "./view/HomePage.vue";
import About from "./view/About.vue";

const activeId = ref('dashboard')
const sidebarCollapsed = ref(false)

const viewMap: Record<string, Component> = {
  homepage: HomePage,
  about: About,
}

const currentView = computed(() => viewMap[activeId.value] || HomePage)
</script>

<template>
  <TitleBar/>
  <div class="app-container">
    <Sidebar
        v-model:active-id="activeId"
        :collapsed="sidebarCollapsed"
        @toggle-collapse="sidebarCollapsed = !sidebarCollapsed"
    />
    <main class="main-content">
      <component :is="currentView" />
    </main>
  </div>
</template>
<style scoped>
.app-container {
  display: flex;
  height: 100vh;
  width: 100vw;
  overflow: hidden;
}

.main-content {
  flex: 1;
  padding: 24px;
  overflow-y: auto;
  overflow-x: hidden;
}
</style>
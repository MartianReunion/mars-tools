<template>
  <aside class="sidebar" :class="{ collapsed: collapsed }">
    <!-- 汉堡切换按钮 -->
    <button
        class="toggle-btn"
        @click="$emit('toggle-collapse')"
        aria-label="切换侧栏"
        type="button"
    >
      <ChevronLeft v-if="!collapsed" :size="20" :stroke-width="2"/>
      <ChevronRight v-else :size="20" :stroke-width="2"/>
    </button>

    <!-- 导航菜单（唯一可滚动区域） -->
    <nav class="sidebar-nav">
      <ul>
        <li
            v-for="item in menuItems"
            :key="item.id"
            class="nav-item"
            :class="{ active: modelValue === item.id }"
            @click="modelValue = item.id"
            role="menuitem"
            tabindex="0"
            @keyup.enter="modelValue = item.id"
            @keyup.space="modelValue = item.id"
        >
          <div class="nav-content">
            <div class="icon-box">
              <component
                  :is="item.icon"
                  :size="18"
                  :stroke-width="2"
                  color="var(--svg-stroke-color)"
              />
            </div>
            <span class="nav-text">{{ item.label }}</span>
          </div>
          <div v-if="modelValue === item.id && !collapsed" class="indicator"/>
        </li>
      </ul>
    </nav>
  </aside>
</template>

<script setup>
import {
  LayoutGrid,
  BarChart3,
  Users,
  Settings,
  ChevronLeft,
  ChevronRight
} from 'lucide-vue-next'

// v-model:activeId 双向绑定
const modelValue = defineModel('activeId', {
  type: String,
  default: 'dashboard'
})

// 折叠状态由父组件控制
defineProps({
  collapsed: {
    type: Boolean,
    default: false
  }
})

// 事件声明
defineEmits(['toggle-collapse'])

// 菜单配置
const menuItems = [
  {id: 'homepage', label: '首页', icon: LayoutGrid},
  {id: 'about', label: '关于', icon: BarChart3}
]
</script>

<style scoped>
.sidebar {
  width: 64px;
  height: 100%;
  background-color: var(--bg-color);
  color: var(--text-color);
  display: flex;
  flex-direction: column;
  border-right: 1px solid var(--border-color);
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  box-sizing: border-box;
  transition: width 0.2s ease;
  position: relative;
  overflow: hidden;
  flex-shrink: 0;
}

/* 展开态宽度 */
.sidebar:not(.collapsed) {
  width: 200px;
}

/* 汉堡切换按钮 */
.toggle-btn {
  height: 48px;
  width: 100%;
  background: transparent;
  border: none;
  border-bottom: 1px solid var(--border-color);
  color: var(--text-color);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  padding: 0;
  transition: background-color 0.2s ease;
}

.toggle-btn:hover {
  background-color: var(--btn-cover-color);
}

.toggle-btn:focus {
  outline: 2px solid var(--text-color);
  outline-offset: -2px;
}

/* 导航区域 - 唯一可滚动部分 */
.sidebar-nav {
  flex: 1;
  padding: 8px 4px;
  overflow-y: auto;
  overflow-x: hidden;
}

.sidebar-nav ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

/* 菜单项 */
.nav-item {
  margin-bottom: 4px;
  border-radius: 6px;
  cursor: pointer;
  transition: background-color 0.2s ease;
  position: relative;
  display: flex;
  align-items: center;
  outline: none;
}

.nav-item:hover {
  background-color: var(--btn-cover-color);
}

.nav-item:focus {
  background-color: var(--btn-cover-color);
}

.nav-item.active {
  background-color: var(--btn-cover-color);
}

/* 激活指示器（仅展开时显示） */
.nav-item.active .indicator {
  position: absolute;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  height: 60%;
  width: 3px;
  background-color: var(--text-color);
  border-radius: 0 4px 4px 0;
}

/* 菜单项内容 */
.nav-content {
  display: flex;
  align-items: center;
  width: 100%;
  padding: 10px 8px;
  white-space: nowrap;
}

/* 图标容器 */
.icon-box {
  flex-shrink: 0;
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto;
}

.sidebar:not(.collapsed) .icon-box {
  margin: 0 12px 0 8px;
}

/* 文字 - 折叠时隐藏 */
.nav-text {
  font-size: 0.9rem;
  font-weight: 500;
  opacity: 1;
  transition: opacity 0.15s ease, width 0.15s ease;
}

.sidebar.collapsed .nav-text {
  opacity: 0;
  width: 0;
  overflow: hidden;
  pointer-events: none;
}

/* 自定义滚动条（暗色主题适配） */
.sidebar-nav::-webkit-scrollbar {
  width: 4px;
}

.sidebar-nav::-webkit-scrollbar-track {
  background: transparent;
}

.sidebar-nav::-webkit-scrollbar-thumb {
  background: var(--btn-cover-color);
  border-radius: 2px;
}

.sidebar-nav::-webkit-scrollbar-thumb:hover {
  background: var(--border-color);
}

/* 隐藏 Firefox 滚动条但保留功能 */
.sidebar-nav {
  scrollbar-width: thin;
  scrollbar-color: var(--btn-cover-color) transparent;
}
</style>
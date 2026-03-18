<script setup lang="ts">
import { ref, onMounted } from 'vue'

// 可选：添加简单的加载动画状态
const isLoaded = ref(false)

onMounted(() => {
  // 微小延迟触发入场动画
  setTimeout(() => {
    isLoaded.value = true
  }, 50)
})
</script>

<template>
  <div class="home-container" :class="{ loaded: isLoaded }">
    <!-- 主内容区：垂直居中 -->
    <main class="home-content">
      <!-- 软件图标 -->
      <div class="icon-wrapper">
        <img
            src="/icon.png"
            alt="火星工具箱图标"
            class="app-icon"
            draggable="false"
        />
        <!-- 微光效果 -->
        <div class="icon-glow" />
      </div>

      <!-- 标题区域 -->
      <div class="title-section">
        <h1 class="app-title">火星工具箱</h1>
        <p class="app-subtitle">一些小工具</p>
      </div>

      <!-- 正文占位（可按需填充功能介绍/公告等） -->
      <div class="content-placeholder">
        <!-- 预留区域：未来可添加功能卡片、更新日志、快捷入口等 -->
      </div>
    </main>

    <!-- 底部信息 -->
    <footer class="home-footer">
      <div class="footer-content">
        <span class="footer-text">你可以审计代码</span>
        <a
            href="https://github.com/MartianReunion/mars-tool"
            target="_blank"
            rel="noopener noreferrer"
            class="audit-link"
        >
          Github仓库 →
        </a>
      </div>
    </footer>
  </div>
</template>

<style scoped>
.home-container {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  background-color: var(--bg-color, #1a1a1a);
  color: var(--text-color, #e0e0e0);
  opacity: 0;
  transform: translateY(8px);
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.home-container.loaded {
  opacity: 1;
  transform: translateY(0);
}

/* 主内容区：垂直水平居中 */
.home-content {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 24px;
  gap: 28px;
}

/* 图标区域 */
.icon-wrapper {
  position: relative;
  width: 120px;
  height: 120px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.app-icon {
  width: 100%;
  height: 100%;
  object-fit: contain;
  border-radius: 20px;
  transition: transform 0.25s ease;
}

.app-icon:hover {
  transform: scale(1.03);
}

/* 图标微光效果（可选装饰） */
.icon-glow {
  position: absolute;
  inset: -8px;
  border-radius: 24px;
  background: radial-gradient(
      circle at center,
      rgba(99, 102, 241, 0.15) 0%,
      transparent 70%
  );
  pointer-events: none;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.icon-wrapper:hover .icon-glow {
  opacity: 1;
}

/* 标题区域 */
.title-section {
  text-align: center;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.app-title {
  font-size: 2rem;
  font-weight: 700;
  margin: 0;
  letter-spacing: 0.5px;
  background: var(--text-color);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.app-subtitle {
  font-size: 1rem;
  color: var(--text-color, #e0e0e0);
  opacity: 0.7;
  margin: 0;
  font-weight: 400;
}

/* 正文占位区 */
.content-placeholder {
  min-height: 60px;
  width: 100%;
  max-width: 520px;
  /* 未来可添加背景/边框作为功能卡片容器 */
}

/* 底部区域 */
.home-footer {
  padding: 16px 24px 20px;
  border-top: 1px solid var(--border-color, #333);
  background-color: var(--bg-color, #1a1a1a);
  display: flex;
  justify-content: center;
}

.footer-content {
  display: flex;
  align-items: center;
  gap: 12px;
  font-size: 0.875rem;
  color: var(--text-color, #e0e0e0);
  opacity: 0.8;
}

.footer-text {
  user-select: none;
}

.audit-link {
  color: #818cf8; /* 柔和的靛蓝色，暗色主题下清晰可读 */
  text-decoration: none;
  font-weight: 500;
  padding: 4px 8px;
  border-radius: 4px;
  transition: all 0.2s ease;
  position: relative;
}

.audit-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 8px;
  right: 8px;
  height: 1px;
  background: currentColor;
  transform: scaleX(0);
  transform-origin: right;
  transition: transform 0.2s ease;
}

.audit-link:hover {
  color: #a5b4fc;
  opacity: 1;
}

.audit-link:hover::after {
  transform: scaleX(1);
  transform-origin: left;
}

.audit-link:active {
  transform: scale(0.98);
}

/* 响应式适配 */
@media (max-width: 480px) {
  .app-title {
    font-size: 1.5rem;
  }

  .app-subtitle {
    font-size: 0.95rem;
  }

  .icon-wrapper {
    width: 96px;
    height: 96px;
  }

  .footer-content {
    flex-direction: column;
    gap: 4px;
    text-align: center;
  }
}

/* 暗色主题滚动条适配（如果内容溢出） */
.home-container::-webkit-scrollbar {
  width: 6px;
}
.home-container::-webkit-scrollbar-track {
  background: transparent;
}
.home-container::-webkit-scrollbar-thumb {
  background: var(--btn-cover-color, #333);
  border-radius: 3px;
}
</style>
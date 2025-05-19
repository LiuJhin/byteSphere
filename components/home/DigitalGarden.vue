<template>
  <section
    class="py-24 relative overflow-hidden bg-gradient-to-b from-gray-900 via-gray-900 to-gray-800"
  >
    <!-- 背景动画 -->
    <CommonCyberGrid class="opacity-3" />
    <CircuitLines class="opacity-20" />

    <!-- 装饰性圆环 -->
    <div
      class="absolute top-20 left-10 w-64 h-64 bg-primary-500/3 rounded-full blur-3xl animate-pulse"
    ></div>
    <div
      class="absolute bottom-20 right-10 w-64 h-64 bg-secondary-500/3 rounded-full blur-3xl animate-pulse delay-1000"
    ></div>

    <!-- 浮动装饰元素 -->
    <div class="absolute top-40 right-20 animate-float-slow">
      <div
        class="w-20 h-20 border border-primary-500/20 rounded-lg rotate-45"
      ></div>
    </div>
    <div class="absolute bottom-40 left-20 animate-float-slow delay-500">
      <div class="w-16 h-16 border border-secondary-500/20 rounded-full"></div>
    </div>

    <!-- 背景渐变 -->
    <div
      class="absolute inset-0 bg-[radial-gradient(circle_at_30%_20%,rgba(79,70,229,0.05)_0%,transparent_50%)]"
    ></div>
    <div
      class="absolute inset-0 bg-[radial-gradient(circle_at_70%_80%,rgba(16,185,129,0.05)_0%,transparent_50%)]"
    ></div>

    <div class="container mx-auto px-4 relative">
      <!-- 标题部分 -->
      <ScrollReveal direction="bottom" :distance="50">
        <div class="relative">
          <h2
            class="text-4xl md:text-5xl font-bold text-center mb-8 relative z-10"
          >
            <span
              class="text-primary-400 inline-block transform hover:scale-110 transition-transform"
              >🌱</span
            >
            <span
              class="text-transparent bg-clip-text bg-gradient-to-r from-primary-400 via-secondary-400 to-primary-400 animate-gradient-x"
            >
              欢迎来到我的数字花园
            </span>
          </h2>
          <!-- 标题装饰线 -->
          <div
            class="absolute -bottom-4 left-1/2 transform -translate-x-1/2 w-40 h-0.5 bg-gradient-to-r from-transparent via-primary-500/50 to-transparent"
          ></div>
        </div>

        <p
          class="text-gray-400 text-lg text-center max-w-3xl mx-auto mb-16 leading-relaxed"
        >
          这里是我记录技术成长、分享前端见解的角落。热爱将设计转化为优雅代码，享受在像素与逻辑之间寻找完美平衡的乐趣。
        </p>
      </ScrollReveal>

      <!-- 主要内容卡片 -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 mb-16">
        <!-- 关于我 -->
        <ScrollReveal direction="left" :distance="100" :delay="0.2">
          <div class="card-container group relative" data-scroll>
            <div class="card-glow"></div>
            <div
              class="bg-gray-900 rounded-xl p-6 border-2 border-gray-700 hover:border-primary-500 transition-all relative z-10"
            >
              <div class="card-header">
                <span
                  class="text-3xl mr-2 transform group-hover:scale-110 transition-transform"
                  >👨‍💻</span
                >
                <h3 class="text-2xl font-semibold text-white">关于我</h3>
              </div>
              <p class="text-gray-400 mb-4 mt-4">
                一名对用户体验有执念的前端开发者，擅长用 React/Vue
                搭建富有生命力的 Web 应用。日常沉迷于：
              </p>
              <ul class="space-y-3 text-gray-300">
                <li
                  class="skill-item group/item"
                  v-for="(skill, index) in skills"
                  :key="skill"
                  :style="{ '--delay': `${index * 0.1}s` }"
                >
                  <span class="skill-dot"></span>
                  <span class="skill-text">{{ skill }}</span>
                </li>
              </ul>
            </div>
          </div>
        </ScrollReveal>

        <!-- 技术手记 -->
        <ScrollReveal direction="bottom" :distance="100" :delay="0.2">
          <div class="card-container group" data-scroll>
            <div class="card-glow"></div>
            <div
              class="bg-gray-800/30 backdrop-blur-sm rounded-xl p-6 border border-gray-700/50 hover:border-secondary-500/50 transition-all relative z-10"
            >
              <div class="card-header">
                <span
                  class="text-3xl mr-2 transform group-hover:scale-110 transition-transform"
                  >✨</span
                >
                <h3 class="text-2xl font-semibold text-white">技术手记</h3>
              </div>
              <p class="text-gray-400 mb-4 mt-4">在这里你会看到：</p>
              <ul class="space-y-3 text-gray-300">
                <li
                  class="note-item group/item"
                  v-for="(note, index) in notes"
                  :key="note"
                  :style="{ '--delay': `${index * 0.1}s` }"
                >
                  <span
                    class="text-secondary-400 mr-2 transform group-hover/item:translate-x-1 transition-transform"
                    >▷</span
                  >
                  <span class="note-text">{{ note }}</span>
                </li>
              </ul>
            </div>
          </div>
        </ScrollReveal>

        <!-- 近期关注 -->
        <ScrollReveal direction="right" :distance="100" :delay="0.2">
          <div class="card-container group" data-scroll>
            <div class="card-glow"></div>
            <div
              class="bg-gray-800/30 backdrop-blur-sm rounded-xl p-6 border border-gray-700/50 hover:border-primary-500/50 transition-all relative z-10"
            >
              <div class="card-header">
                <span
                  class="text-3xl mr-2 transform group-hover:scale-110 transition-transform"
                  >🚀</span
                >
                <h3 class="text-2xl font-semibold text-white">近期关注</h3>
              </div>
              <ul class="space-y-4 text-gray-300 mt-4">
                <li
                  class="focus-item group/item"
                  v-for="(focus, index) in focuses"
                  :key="focus"
                  :style="{ '--delay': `${index * 0.1}s` }"
                >
                  <div class="focus-dot"></div>
                  <span class="focus-text">{{ focus }}</span>
                </li>
              </ul>
            </div>
          </div>
        </ScrollReveal>
      </div>

      <!-- 与我连接 -->
      <ScrollReveal direction="bottom" :distance="50" :delay="0.8">
        <div class="max-w-2xl mx-auto text-center">
          <div class="connect-header mb-8">
            <span
              class="text-3xl transform hover:scale-110 transition-transform inline-block"
              >📮</span
            >
            <h3 class="text-2xl font-semibold text-white ml-2 inline-block">
              与我连接
            </h3>
          </div>

          <p class="text-gray-400 mb-8">当我不在敲代码时，可能在：</p>

          <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mb-12">
            <div class="hobby-card" v-for="hobby in hobbies" :key="hobby.text">
              <span class="hobby-icon">{{ hobby.icon }}</span>
              <span class="hobby-text">{{ hobby.text }}</span>
            </div>
          </div>

          <div class="flex flex-wrap justify-center gap-4">
            <a
              v-for="action in actions"
              :key="action.text"
              :href="action.link"
              :class="['action-button', action.type]"
            >
              <span class="button-icon">{{ action.icon }}</span>
              <span class="button-text">{{ action.text }}</span>
            </a>
          </div>
        </div>
      </ScrollReveal>
    </div>
  </section>
</template>

<script setup lang="ts">
import ScrollReveal from "~/components/animations/ScrollReveal.vue";
import CircuitLines from "~/components/animations/CircuitLines.vue";

const skills = [
  "组件化设计的哲学思考",
  "CSS 魔法与动画微交互",
  "性能优化的毫米级雕琢",
  "TypeScript 的类型体操训练",
];

const notes = [
  "前沿技术深度实践",
  "反直觉的浏览器运行机制图解",
  "优雅代码的炼成方法论",
  "开源项目踩坑实录",
];

const focuses = [
  "探索 Three.js 的 3D 可视化可能性",
  "用 Rust 重写前端工具链的实践",
  "Web Components 的生态突围战",
  "如何设计自解释的 API 接口",
];

const hobbies = [
  { icon: "🎨", text: "拆解交互动画" },
  { icon: "🔧", text: "提交开源PR" },
  { icon: "✏️", text: "素描界面布局" },
  { icon: "🎹", text: "收集键盘声响" },
];

const actions = [
  { icon: "📚", text: "查看最新文章", link: "#", type: "primary" },
  { icon: "🛠️", text: "探索我的项目", link: "#", type: "secondary" },
  { icon: "📝", text: "技术简历通道", link: "#", type: "primary" },
];

// 监听滚动事件，添加视差效果
onMounted(() => {
  const cards = document.querySelectorAll("[data-scroll]");

  const handleScroll = () => {
    cards.forEach((card) => {
      if (card instanceof HTMLElement) {
        const rect = card.getBoundingClientRect();
        const isVisible = rect.top < window.innerHeight && rect.bottom > 0;

        if (isVisible) {
          const scrolled = window.scrollY;
          const rate = scrolled * 0.05;
          card.style.transform = `translateY(${rate}px)`;
        }
      }
    });
  };

  window.addEventListener("scroll", handleScroll);
  handleScroll(); // 初始化位置
});
</script>

<style scoped>
.backdrop-blur-sm {
  backdrop-filter: blur(8px);
}

/* 卡片容器和发光效果 */
.card-container {
  position: relative;
  transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
  border-radius: 0.75rem;
  background: #111827; /* 深色实体背景 */
  box-shadow: 0 0 0 1px rgba(255, 255, 255, 0.1),
    0 4px 6px -1px rgba(0, 0, 0, 0.5), 0 2px 4px -1px rgba(0, 0, 0, 0.3);
}

.card-container:hover {
  transform: translateY(-5px);
  box-shadow: 0 0 0 2px rgba(var(--primary-rgb), 0.3),
    0 10px 15px -3px rgba(0, 0, 0, 0.5), 0 4px 6px -2px rgba(0, 0, 0, 0.3);
}

.backdrop-blur-xl {
  backdrop-filter: blur(16px);
}

/* 增强卡片内容的对比度 */
.text-gray-400 {
  color: rgba(209, 213, 219, 1); /* 更亮的文字颜色 */
}

.text-gray-300 {
  color: rgba(229, 231, 235, 1); /* 更亮的文字颜色 */
}

.card-glow {
  position: absolute;
  inset: -1px;
  background: radial-gradient(
    circle at var(--mouse-x, 50%) var(--mouse-y, 50%),
    rgba(var(--primary-rgb), 0.15),
    /* 增加发光强度 */ transparent 100%
  );
  opacity: 0;
  transition: opacity 0.3s ease;
  border-radius: 0.75rem;
  z-index: 0;
}

.card-container:hover .card-glow {
  opacity: 1;
}

/* 卡片头部样式 */
.card-header {
  display: flex;
  align-items: center;
  padding-bottom: 1rem;
  border-bottom: 2px solid rgba(255, 255, 255, 0.1); /* 更明显的分隔线 */
}

/* 技能项样式 */
.skill-item {
  display: flex;
  align-items: center;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  animation: slideIn 0.5s ease-out backwards;
  animation-delay: var(--delay);
}

.skill-dot {
  width: 8px;
  height: 8px;
  background: rgba(var(--primary-rgb), 0.5);
  border-radius: 50%;
  margin-right: 12px;
  transition: all 0.3s ease;
}

.skill-item:hover .skill-dot {
  background: rgb(var(--primary-rgb));
  box-shadow: 0 0 8px rgba(var(--primary-rgb), 0.5);
}

/* 笔记项样式 */
.note-item {
  display: flex;
  align-items: center;
  transition: all 0.3s ease;
  animation: slideIn 0.5s ease-out backwards;
  animation-delay: var(--delay);
}

.note-item:hover {
  color: rgb(var(--secondary-rgb));
  transform: translateX(10px);
}

/* 关注项样式 */
.focus-item {
  display: flex;
  align-items: start;
  gap: 12px;
  transition: all 0.3s ease;
  animation: slideIn 0.5s ease-out backwards;
  animation-delay: var(--delay);
}

.focus-dot {
  width: 8px;
  height: 8px;
  background: rgba(var(--primary-rgb), 0.5);
  border-radius: 50%;
  margin-top: 8px;
  transition: all 0.3s ease;
}

.focus-item:hover .focus-dot {
  background: rgb(var(--primary-rgb));
  box-shadow: 0 0 8px rgba(var(--primary-rgb), 0.5);
}

/* 爱好卡片样式 */
.hobby-card {
  @apply px-4 py-3 bg-gray-800/30 rounded-lg text-gray-300 hover:bg-gray-800/50 transition-all flex flex-col items-center gap-2;
  animation: fadeIn 0.5s ease-out backwards;
  animation-delay: calc(var(--delay) + 0.2s);
}

.hobby-card:hover {
  transform: translateY(-5px);
  background: rgba(var(--primary-rgb), 0.1);
}

/* 动作按钮样式 */
.action-button {
  @apply px-6 py-3 rounded-lg transition-all flex items-center gap-2;
  position: relative;
  overflow: hidden;
}

.action-button::before {
  content: "";
  position: absolute;
  inset: 0;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(255, 255, 255, 0.1),
    transparent
  );
  transform: translateX(-100%);
  transition: transform 0.5s;
}

.action-button:hover::before {
  transform: translateX(100%);
}

.action-button.primary {
  @apply bg-primary-500/10 text-primary-400 hover:bg-primary-500/20;
}

.action-button.secondary {
  @apply bg-secondary-500/10 text-secondary-400 hover:bg-secondary-500/20;
}

/* 动画 */
@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateX(-20px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes float-slow {
  0%,
  100% {
    transform: translateY(0) rotate(0deg);
  }
  50% {
    transform: translateY(-20px) rotate(5deg);
  }
}

.animate-float-slow {
  animation: float-slow 6s ease-in-out infinite;
}

.animate-gradient-x {
  background-size: 200% 100%;
  animation: gradient-x 15s ease infinite;
}

@keyframes gradient-x {
  0%,
  100% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
}

:root {
  --primary-rgb: 79, 70, 229;
  --secondary-rgb: 16, 185, 129;
}

/* 调整背景渐变的不透明度 */
.bg-gradient-to-b {
  background: linear-gradient(to bottom, #111827 0%, #1f2937 100%);
}

/* 减弱背景动画的干扰 */
.opacity-5 {
  opacity: 0.03;
}

.opacity-30 {
  opacity: 0.1;
}
</style>

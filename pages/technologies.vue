<script setup lang="ts">
import { ref, onMounted } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import ScrollReveal from "~/components/animations/ScrollReveal.vue";

gsap.registerPlugin(ScrollTrigger);

const techStackRef = ref<HTMLElement | null>(null);

const technologies = [
  {
    name: "Vue.js 3",
    description: "基于组合式API的现代化前端框架，提供卓越的性能和开发体验",
    icon: "🧩",
    category: "前端框架",
  },
  {
    name: "Nuxt 3",
    description: "基于Vue的全栈框架，支持SSR、静态生成和API自动生成",
    icon: "⚡",
    category: "全栈框架",
  },
  {
    name: "TypeScript",
    description: "为JavaScript添加静态类型检查，提高代码质量和开发效率",
    icon: "📝",
    category: "编程语言",
  },
  {
    name: "Tailwind CSS",
    description: "实用优先的CSS框架，通过类名快速构建现代UI",
    icon: "🎨",
    category: "样式框架",
  },
  {
    name: "GSAP",
    description: "专业级网页动画库，提供流畅、高性能的动画效果",
    icon: "✨",
    category: "动画库",
  },
  {
    name: "WebGL",
    description: "基于OpenGL的JavaScript API，用于在浏览器中渲染3D图形",
    icon: "🌐",
    category: "图形渲染",
  },
  {
    name: "WebSockets",
    description: "提供全双工通信通道的网络协议，实现实时数据传输",
    icon: "🔄",
    category: "网络协议",
  },
  {
    name: "Node.js",
    description: "基于Chrome V8引擎的JavaScript运行环境，用于构建服务器端应用",
    icon: "🖥️",
    category: "服务器环境",
  },
];

onMounted(() => {
  // 技术栈卡片动画
  const cards = techStackRef.value?.querySelectorAll(".tech-card");
  cards?.forEach((card, index) => {
    gsap.from(card, {
      scrollTrigger: {
        trigger: card,
        start: "top 80%",
      },
      opacity: 0,
      y: 30,
      duration: 0.6,
      delay: index * 0.1,
    });
  });
});
</script>

<template>
  <div class="bg-gray-900 min-h-screen">
    <!-- 页面标题 -->
    <section class="pt-32 pb-16 px-4 relative overflow-hidden">
      <div
        class="absolute inset-0 bg-gradient-to-b from-primary-900/30 to-gray-900/0"
      ></div>
      <div class="container mx-auto text-center relative z-10">
        <h1 class="text-4xl md:text-6xl font-bold text-white mb-6">
          <span
            class="text-transparent bg-clip-text bg-gradient-to-r from-primary-400 to-secondary-400"
            >技术</span
          >
          驱动未来
        </h1>
        <p class="text-xl text-gray-300 max-w-3xl mx-auto">
          探索ByteSphere背后的核心技术栈，这些现代化工具和框架使我们能够创造出流畅、沉浸式的游戏体验
        </p>
      </div>
    </section>

    <!-- 技术栈展示 -->
    <section class="py-16 px-4">
      <div class="container mx-auto">
        <div
          ref="techStackRef"
          class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6"
        >
          <div
            v-for="(tech, index) in technologies"
            :key="index"
            class="tech-card bg-gray-800 rounded-xl p-6 border border-gray-700 hover:border-primary-500 transition-all duration-300 hover:shadow-lg hover:shadow-primary-500/20"
          >
            <div class="text-4xl mb-4">{{ tech.icon }}</div>
            <div class="text-sm text-primary-400 mb-2">{{ tech.category }}</div>
            <h3 class="text-xl font-bold text-white mb-2">{{ tech.name }}</h3>
            <p class="text-gray-400">{{ tech.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- 技术理念 -->
    <ScrollReveal direction="bottom" :distance="50">
      <section class="py-16 px-4 bg-gray-800">
        <div class="container mx-auto">
          <div class="max-w-3xl mx-auto text-center mb-12">
            <h2 class="text-3xl font-bold text-white mb-6">我们的技术理念</h2>
            <p class="text-gray-300">
              在ByteSphere，我们坚信技术不仅是工具，更是创造力的催化剂。我们精心选择每一项技术，确保它们能够协同工作，为用户带来最佳体验。
            </p>
          </div>

          <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
            <div class="bg-gray-900 p-6 rounded-xl border border-gray-700">
              <h3 class="text-xl font-bold text-white mb-3">性能优先</h3>
              <p class="text-gray-400">
                我们优化每一行代码，确保游戏在各种设备上都能流畅运行，无论是高端PC还是移动设备。
              </p>
            </div>
            <div class="bg-gray-900 p-6 rounded-xl border border-gray-700">
              <h3 class="text-xl font-bold text-white mb-3">用户体验至上</h3>
              <p class="text-gray-400">
                从加载时间到交互反馈，我们关注每一个细节，打造沉浸式、直观的用户界面。
              </p>
            </div>
            <div class="bg-gray-900 p-6 rounded-xl border border-gray-700">
              <h3 class="text-xl font-bold text-white mb-3">持续创新</h3>
              <p class="text-gray-400">
                我们不断探索新技术和方法，将最前沿的解决方案融入我们的产品中。
              </p>
            </div>
          </div>
        </div>
      </section>
    </ScrollReveal>

    <!-- 返回主页 -->
    <div class="container mx-auto py-12 text-center">
      <NuxtLink
        to="/"
        class="inline-block bg-primary-500 hover:bg-primary-600 text-white px-8 py-3 rounded-lg text-lg font-medium transition-all transform hover:scale-105"
      >
        返回首页
      </NuxtLink>
    </div>
  </div>
</template>

<style scoped>
.tech-card {
  backdrop-filter: blur(10px);
  transition: all 0.3s ease;
}

.tech-card:hover {
  transform: translateY(-5px);
}
</style>

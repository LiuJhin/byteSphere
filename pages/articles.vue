<script setup lang="ts">
import { ref, onMounted } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import ScrollReveal from "~/components/animations/ScrollReveal.vue";

gsap.registerPlugin(ScrollTrigger);

const articlesRef = ref<HTMLElement | null>(null);

const articles = [
  {
    id: 1,
    title: "游戏开发中的粒子系统优化",
    description:
      "探索如何在Web游戏中实现高效的粒子系统，提升视觉效果的同时保持流畅性能",
    date: "2023-12-15",
    category: "技术分享",
    image: "/images/particle-system.jpg",
  },
  {
    id: 2,
    title: "CSS量子化系统与现代Web设计",
    description:
      "深入了解CSS量子化系统如何改变Web设计范式，创造出更具沉浸感的用户界面",
    date: "2023-11-28",
    category: "设计理念",
    image: "/images/css-quantum.jpg",
  },
  {
    id: 3,
    title: "JavaScript语法糖的演进历程",
    description:
      "从ES6到现在，JavaScript语法糖如何改变了我们的编码方式和开发效率",
    date: "2023-11-10",
    category: "编程语言",
    image: "/images/js-syntax.jpg",
  },
  {
    id: 4,
    title: "浏览器画布上的数字艺术",
    description: "Canvas和WebGL如何为现代Web应用带来前所未有的创意表达空间",
    date: "2023-10-25",
    category: "创意技术",
    image: "/images/digital-art.jpg",
  },
  {
    id: 5,
    title: "交互设计中的哲学思考",
    description:
      "探讨用户交互设计背后的哲学原则，以及如何将这些原则应用到游戏开发中",
    date: "2023-10-12",
    category: "用户体验",
    image: "/images/interaction-philosophy.jpg",
  },
  {
    id: 6,
    title: "WebAssembly与游戏性能优化",
    description:
      "如何利用WebAssembly突破JavaScript性能瓶颈，为Web游戏带来接近原生的体验",
    date: "2023-09-30",
    category: "性能优化",
    image: "/images/wasm-games.jpg",
  },
];

onMounted(() => {
  // 文章卡片动画
  const cards = articlesRef.value?.querySelectorAll(".article-card");
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
            >文章</span
          >
          与洞见
        </h1>
        <p class="text-xl text-gray-300 max-w-3xl mx-auto">
          探索ByteSphere的技术文章、设计理念和创意思考，深入了解数字创作的无限可能
        </p>
      </div>
    </section>

    <!-- 文章列表 -->
    <section class="py-16 px-4" ref="articlesRef">
      <div class="container mx-auto">
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div
            v-for="article in articles"
            :key="article.id"
            class="article-card bg-gray-800 rounded-xl overflow-hidden shadow-lg transition-all duration-300 hover:shadow-primary-500/20 hover:translate-y-[-5px]"
          >
            <div class="h-48 bg-gray-700 relative overflow-hidden">
              <!-- 图片占位符 -->
              <div
                class="absolute inset-0 flex items-center justify-center text-4xl"
              >
                {{ article.category.charAt(0) }}
              </div>
              <!-- 分类标签 -->
              <div
                class="absolute top-4 right-4 bg-primary-500 text-white text-xs font-bold px-3 py-1 rounded-full"
              >
                {{ article.category }}
              </div>
            </div>
            <div class="p-6">
              <div class="text-gray-400 text-sm mb-2">{{ article.date }}</div>
              <h3 class="text-xl font-bold text-white mb-3 line-clamp-2">
                {{ article.title }}
              </h3>
              <p class="text-gray-300 mb-4 line-clamp-3">
                {{ article.description }}
              </p>
              <NuxtLink
                :to="`/detail/${article.id}`"
                class="inline-block text-primary-400 hover:text-primary-300 font-medium"
              >
                阅读全文 →
              </NuxtLink>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
.article-card {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.line-clamp-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.line-clamp-3 {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>

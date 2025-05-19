<template>
  <section
    class="relative h-screen flex items-center justify-center overflow-hidden bg-gray-900"
  >
    <!-- 背景动画 -->
    <div class="absolute inset-0 z-0">
      <ClientOnly>
        <div
          v-if="isMounted"
          ref="particles"
          class="absolute inset-0 opacity-20"
        ></div>
      </ClientOnly>
      <div
        class="absolute inset-0 bg-gradient-to-b from-primary-900/50 to-gray-900"
      ></div>
    </div>

    <!-- 主要内容 -->
    <div class="relative z-10 text-center px-4">
      <h1
        ref="titleRef"
        :class="[
          'text-4xl md:text-6xl lg:text-7xl font-bold text-white mb-6',
          { 'opacity-0': !isMounted },
        ]"
      >
        Welcome to
        <span
          class="text-transparent bg-clip-text bg-gradient-to-r from-primary-400 to-secondary-400"
          >ByteSphere</span
        >
      </h1>
      <p
        ref="subtitleRef"
        :class="[
          'text-xl md:text-2xl text-gray-300 mb-8 max-w-2xl mx-auto',
          { 'opacity-0': !isMounted },
        ]"
      >
        在浏览器画布上编织逻辑与美感的数字经纬，当CSS量子化系统邂逅JS语法糖的浪漫，每个编译成真理的像素都在与亿万用户展开一场关于交互哲学的对话
      </p>
      <div ref="buttonsRef" :class="['space-x-4', { 'opacity-0': !isMounted }]">
        <button
          class="btn bg-primary-500 hover:bg-primary-600 text-white px-8 py-3 rounded-lg text-lg font-medium transition-all transform hover:scale-105"
        >
          开始探索
        </button>
        <button
          class="btn bg-gray-800 hover:bg-gray-700 text-white px-8 py-3 rounded-lg text-lg font-medium transition-all transform hover:scale-105"
        >
          了解更多
        </button>
      </div>
    </div>

    <!-- 向下滚动指示器 -->
    <div
      ref="scrollIndicatorRef"
      :class="[
        'absolute bottom-8 left-1/2 transform -translate-x-1/2',
        { 'opacity-0': !isMounted },
      ]"
    >
      <div class="animate-bounce">
        <svg
          class="w-6 h-6 text-white"
          fill="none"
          stroke="currentColor"
          viewBox="0 0 24 24"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M19 14l-7 7m0 0l-7-7m7 7V3"
          />
        </svg>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted, nextTick } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

const isMounted = ref(false);
const titleRef = ref<HTMLElement | null>(null);
const subtitleRef = ref<HTMLElement | null>(null);
const buttonsRef = ref<HTMLElement | null>(null);
const scrollIndicatorRef = ref<HTMLElement | null>(null);
const particles = ref<HTMLElement | null>(null);

// 粒子动画
const createParticle = () => {
  if (!particles.value || !isMounted.value) return;
  const particle = document.createElement("div");
  particle.className = "absolute w-2 h-2 bg-white rounded-full";

  // 随机起始位置
  const startX = Math.random() * window.innerWidth;
  const startY = window.innerHeight + 10;

  particle.style.left = `${startX}px`;
  particle.style.top = `${startY}px`;

  particles.value.appendChild(particle);

  // 动画
  gsap.to(particle, {
    y: -window.innerHeight - 10,
    x: `random(-100, 100)`,
    duration: "random(3, 6)",
    ease: "none",
    onComplete: () => {
      particle.remove();
    },
  });
};

onMounted(async () => {
  // 确保在客户端
  if (typeof window === "undefined") return;

  // 注册 GSAP 插件
  if (typeof gsap.registerPlugin === "function") {
    gsap.registerPlugin(ScrollTrigger);
  }

  // 等待下一个 tick，确保 DOM 完全更新
  await nextTick();
  isMounted.value = true;

  // 入场动画
  await nextTick();
  const tl = gsap.timeline({ defaults: { ease: "power3.out" } });

  tl.to(titleRef.value, {
    opacity: 1,
    y: 0,
    duration: 1,
    from: { y: 50 },
  })
    .to(
      subtitleRef.value,
      {
        opacity: 1,
        y: 0,
        duration: 1,
        from: { y: 30 },
      },
      "-=0.5"
    )
    .to(
      buttonsRef.value,
      {
        opacity: 1,
        y: 0,
        duration: 1,
        from: { y: 30 },
      },
      "-=0.5"
    )
    .to(
      scrollIndicatorRef.value,
      {
        opacity: 0.7,
        duration: 1,
      },
      "-=0.5"
    );

  // 持续创建粒子
  const particleInterval = setInterval(createParticle, 200);

  // 清理函数
  return () => {
    clearInterval(particleInterval);
    isMounted.value = false;
  };
});
</script>

<style scoped>
.btn {
  text-shadow: 0 1px 3px rgba(0, 0, 0, 0.3);
}
</style>

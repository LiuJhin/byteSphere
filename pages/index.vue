<script setup lang="ts">
import { ref, onMounted } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

const communityTextRef = ref<HTMLElement | null>(null);
const communityImageRef = ref<HTMLElement | null>(null);
const featuresRef = ref<HTMLElement | null>(null);

const features = [
  {
    title: "实时对战",
    description: "享受流畅的实时对战体验，与全球玩家一较高下",
    icon: "IconSword",
  },
  {
    title: "云存档",
    description: "游戏进度自动同步到云端，随时随地继续您的游戏",
    icon: "IconCloud",
  },
  {
    title: "社交系统",
    description: "添加好友，组队游戏，分享您的游戏时刻",
    icon: "IconUsers",
  },
  {
    title: "排行榜",
    description: "实时更新的全球排行榜，展示您的游戏实力",
    icon: "IconTrophy",
  },
  {
    title: "成就系统",
    description: "完成各种挑战，解锁独特成就和奖励",
    icon: "IconStar",
  },
  {
    title: "赛事活动",
    description: "参与定期举办的游戏赛事，赢取丰厚奖励",
    icon: "IconEvent",
  },
];

onMounted(() => {
  // 社区部分动画
  gsap.from(communityTextRef.value, {
    scrollTrigger: {
      trigger: communityTextRef.value,
      start: "top 80%",
    },
    opacity: 0,
    x: -50,
    duration: 1,
  });

  gsap.from(communityImageRef.value, {
    scrollTrigger: {
      trigger: communityImageRef.value,
      start: "top 80%",
    },
    opacity: 0,
    x: 50,
    duration: 1,
  });

  // 特性卡片动画
  const cards = featuresRef.value?.querySelectorAll(".feature-card");
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
  <div class="bg-gray-900">
    <!-- Hero Section -->
    <HomeHeroSection />

    <!-- Featured Games -->
    <HomeFeaturedGames />

    <!-- Community Section -->
    <section class="py-20 bg-gray-800">
      <div class="container mx-auto px-4">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-12 items-center">
          <div ref="communityTextRef">
            <h2 class="text-3xl md:text-4xl font-bold text-white mb-6">
              加入我们的游戏社区
            </h2>
            <p class="text-gray-300 text-lg mb-8">
              与数百万玩家一起分享游戏体验，结交新朋友，参与精彩的社区活动。
            </p>
            <button
              class="btn bg-secondary-500 hover:bg-secondary-600 text-white px-8 py-3 rounded-lg text-lg font-medium transition-all transform hover:scale-105"
            >
              立即加入
            </button>
          </div>
          <div ref="communityImageRef" class="relative">
            <div
              class="aspect-video rounded-xl overflow-hidden bg-gradient-to-br from-primary-500/30 to-secondary-500/30"
            >
              <div
                class="absolute inset-0 bg-[radial-gradient(circle_at_center,rgba(255,255,255,0.1)_0%,transparent_70%)] animate-pulse"
              ></div>
              <div class="absolute inset-0 flex items-center justify-center">
                <div class="grid grid-cols-3 gap-4 p-8">
                  <div
                    v-for="n in 9"
                    :key="n"
                    class="w-8 h-8 rounded-full bg-white/10 animate-float"
                    :style="{ animationDelay: `${n * 0.2}s` }"
                  ></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Features Grid -->
    <section class="py-20 bg-gray-900">
      <div class="container mx-auto px-4">
        <div
          ref="featuresRef"
          class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8"
        >
          <div
            v-for="feature in features"
            :key="feature.title"
            class="feature-card p-6 rounded-xl bg-gray-800 border border-gray-700"
          >
            <div class="text-primary-400 mb-4">
              <component :is="feature.icon" class="w-8 h-8" />
            </div>
            <h3 class="text-xl font-semibold text-white mb-3">
              {{ feature.title }}
            </h3>
            <p class="text-gray-400">{{ feature.description }}</p>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
.feature-card {
  transition: all 0.3s ease;
}

.feature-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
  border-color: var(--primary-color);
}

@keyframes float {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

.animate-float {
  animation: float 3s ease-in-out infinite;
}
</style>

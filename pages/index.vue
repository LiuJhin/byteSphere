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
    <section class="py-20 bg-gray-800 relative overflow-hidden">
      <div
        class="absolute inset-0 bg-[radial-gradient(circle_at_top_right,rgba(79,70,229,0.1)_0%,transparent_50%)]"
      ></div>
      <div class="container mx-auto px-4 relative">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-12 items-center">
          <div ref="communityTextRef">
            <h2
              class="glowing-text text-3xl md:text-4xl font-bold text-white mb-6 relative"
            >
              加入我们的
              <span
                class="text-transparent bg-clip-text bg-gradient-to-r from-primary-400 to-secondary-400 animate-gradient-x"
                >游戏社区</span
              >
            </h2>
            <p class="text-gray-300 text-lg mb-8 typing-text">
              与数百万玩家一起分享游戏体验，结交新朋友，参与精彩的社区活动。
            </p>
            <button
              class="btn bg-secondary-500 hover:bg-secondary-600 text-white px-8 py-3 rounded-lg text-lg font-medium transition-all transform hover:scale-105 hover:rotate-1"
            >
              立即加入
              <span
                class="ml-2 inline-block transform hover:translate-x-1 transition-transform"
                >→</span
              >
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
                    :style="{
                      animationDelay: `${n * 0.2}s`,
                      backgroundColor: `rgba(255,255,255,${
                        0.1 + (n % 3) * 0.1
                      })`,
                    }"
                  ></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 波浪效果 -->
    <div class="relative h-32 overflow-hidden">
      <CommonWaveEffect :width="1920" :height="128" />
    </div>

    <!-- Features Grid -->
    <section class="py-20 bg-gray-900 relative overflow-hidden">
      <!-- 背景网格 -->
      <CommonCyberGrid class="opacity-20" />

      <div
        class="absolute inset-0 bg-[radial-gradient(ellipse_at_center,rgba(79,70,229,0.15)_0%,transparent_70%)]"
      ></div>
      <div class="container mx-auto px-4 relative">
        <div class="flex items-center justify-center mb-16">
          <CommonCircleLoader :size="60" class="mr-4" />
          <h2 class="text-4xl md:text-5xl font-bold text-center cyber-text">
            游戏特性
            <div class="cyber-line"></div>
          </h2>
        </div>

        <div
          ref="featuresRef"
          class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8"
        >
          <div
            v-for="(feature, index) in features"
            :key="feature.title"
            class="feature-card group"
            :style="{ animationDelay: `${index * 0.1}s` }"
          >
            <div
              class="relative p-6 bg-gray-800 rounded-xl border border-gray-700 overflow-hidden transition-all duration-500 hover:border-primary-500"
            >
              <div
                class="absolute inset-0 bg-gradient-to-br from-primary-500/10 to-secondary-500/10 opacity-0 group-hover:opacity-100 transition-opacity"
              ></div>

              <!-- 发光边框效果 -->
              <div class="glow-border"></div>

              <!-- 图标容器 -->
              <div class="relative z-10">
                <div
                  class="text-primary-400 mb-4 transform group-hover:scale-110 group-hover:rotate-12 transition-transform duration-500"
                >
                  <component :is="feature.icon" class="w-8 h-8" />
                </div>

                <!-- 标题和描述 -->
                <h3
                  class="text-xl font-semibold text-white mb-3 group-hover:text-primary-400 transition-colors"
                >
                  {{ feature.title }}
                </h3>
                <p
                  class="text-gray-400 group-hover:text-gray-300 transition-colors"
                >
                  {{ feature.description }}
                </p>

                <!-- 悬停时显示的箭头 -->
                <div
                  class="absolute bottom-4 right-4 opacity-0 group-hover:opacity-100 transform group-hover:translate-x-0 translate-x-4 transition-all duration-300"
                >
                  <svg
                    class="w-6 h-6 text-primary-400"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M17 8l4 4m0 0l-4 4m4-4H3"
                    />
                  </svg>
                </div>
              </div>
            </div>
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
}

.glow-border {
  position: absolute;
  inset: -1px;
  background: linear-gradient(
    45deg,
    transparent,
    var(--primary-color),
    transparent
  );
  opacity: 0;
  transition: opacity 0.3s;
  border-radius: inherit;
  z-index: 0;
}

.feature-card:hover .glow-border {
  opacity: 0.5;
  animation: border-glow 2s linear infinite;
}

@keyframes border-glow {
  0%,
  100% {
    clip-path: inset(0 0 98% 0);
  }
  25% {
    clip-path: inset(0 98% 0 0);
  }
  50% {
    clip-path: inset(98% 0 0 0);
  }
  75% {
    clip-path: inset(0 0 0 98%);
  }
}

@keyframes float {
  0%,
  100% {
    transform: translateY(0) rotate(0deg);
  }
  50% {
    transform: translateY(-10px) rotate(5deg);
  }
}

.animate-float {
  animation: float 3s ease-in-out infinite;
}

.glowing-text {
  text-shadow: 0 0 10px rgba(79, 70, 229, 0.5);
}

.cyber-text {
  position: relative;
  display: inline-block;
  background: linear-gradient(45deg, #4f46e5, #10b981);
  -webkit-background-clip: text;
  color: transparent;
  text-shadow: 2px 2px 10px rgba(79, 70, 229, 0.3);
}

.cyber-line {
  height: 2px;
  background: linear-gradient(
    90deg,
    transparent,
    #4f46e5,
    #10b981,
    transparent
  );
  margin-top: 8px;
  transform-origin: left;
  animation: line-grow 2s ease-out forwards;
}

@keyframes line-grow {
  from {
    transform: scaleX(0);
  }
  to {
    transform: scaleX(1);
  }
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

.typing-text {
  overflow: hidden;
  border-right: 2px solid transparent;
  white-space: nowrap;
  animation: typing 3s steps(40, end), blink-caret 0.75s step-end infinite;
}

@keyframes typing {
  from {
    width: 0;
  }
  to {
    width: 100%;
  }
}

@keyframes blink-caret {
  from,
  to {
    border-color: transparent;
  }
  50% {
    border-color: #4f46e5;
  }
}
</style>

<template>
  <section class="py-20 bg-gray-900">
    <div class="container mx-auto px-4">
      <h2
        ref="titleRef"
        class="text-3xl md:text-4xl font-bold text-center text-white mb-12"
      >
        项目展示
      </h2>

      <div
        ref="gamesRef"
        class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8"
      >
        <div
          v-for="game in games"
          :key="game.id"
          class="game-card bg-gray-800 rounded-xl overflow-hidden transform transition-all duration-300 hover:scale-105"
        >
          <div class="relative aspect-video overflow-hidden">
            <div
              class="absolute inset-0 bg-gradient-to-br from-primary-500/20 to-secondary-500/20 animate-gradient"
            ></div>
            <div class="absolute inset-0 flex items-center justify-center">
              <span class="text-4xl text-white/30">{{ game.title[0] }}</span>
            </div>
            <div
              class="absolute inset-0 bg-gradient-to-t from-gray-900 to-transparent"
            ></div>
          </div>
          <div class="p-6">
            <h3 class="text-xl font-semibold text-white mb-2">
              {{ game.title }}
            </h3>
            <p class="text-gray-400 text-sm mb-4">{{ game.description }}</p>
            <div class="flex items-center justify-between">
              <span class="text-primary-400 font-medium">{{ game.genre }}</span>
              <NuxtLink
                :to="`/detail/${game.id}`"
                class="btn bg-primary-500 hover:bg-primary-600 text-white px-4 py-2 rounded-lg text-sm transition-colors"
              >
                了解更多
              </NuxtLink>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

const titleRef = ref<HTMLElement | null>(null);
const gamesRef = ref<HTMLElement | null>(null);

const games = ref([
  {
    id: "1",
    title: "字节球大冒险",
    description:
      "一个充满趣味性的休闲游戏，在这里你将操控字节球进行各种有趣的冒险。",
    genre: "休闲游戏",
    coverImage: "/images/games/game1.jpg",
  },
  {
    id: "2",
    title: "代码勇士",
    description: "在这个编程世界中，你将成为一名代码勇士，解决各种编程难题。",
    genre: "教育游戏",
    coverImage: "/images/games/game2.jpg",
  },
  {
    id: "3",
    title: "像素方块",
    description: "一个创意十足的像素风格游戏，让你体验不一样的方块世界。",
    genre: "创意游戏",
    coverImage: "/images/games/game3.jpg",
  },
]);

onMounted(() => {
  // 标题动画
  gsap.from(titleRef.value, {
    scrollTrigger: {
      trigger: titleRef.value,
      start: "top 80%",
    },
    opacity: 0,
    y: 30,
    duration: 1,
  });

  // 游戏卡片动画
  const cards = gamesRef.value?.querySelectorAll(".game-card");
  cards?.forEach((card, index) => {
    gsap.from(card, {
      scrollTrigger: {
        trigger: card,
        start: "top 80%",
      },
      opacity: 0,
      y: 50,
      duration: 0.8,
      delay: index * 0.2,
    });
  });
});
</script>

<style scoped>
.game-card {
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
    0 2px 4px -1px rgba(0, 0, 0, 0.06);
}

@keyframes gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

.animate-gradient {
  background-size: 200% 200%;
  animation: gradient 15s ease infinite;
}
</style>

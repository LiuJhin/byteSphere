<template>
  <svg
    :width="size"
    :height="size"
    viewBox="0 0 100 100"
    xmlns="http://www.w3.org/2000/svg"
    class="transform"
    :class="{ 'animate-spin': spin }"
  >
    <!-- 外圈 -->
    <circle
      cx="50"
      cy="50"
      r="45"
      fill="none"
      stroke="currentColor"
      stroke-width="2"
      class="text-gray-700"
    />

    <!-- 动态圆弧 -->
    <circle
      cx="50"
      cy="50"
      r="45"
      fill="none"
      stroke="currentColor"
      stroke-width="2"
      stroke-linecap="round"
      class="text-primary-500"
      :stroke-dasharray="circumference"
      :stroke-dashoffset="currentOffset"
    >
      <animate
        attributeName="stroke-dashoffset"
        :values="`${circumference};0`"
        dur="2s"
        repeatCount="indefinite"
        calcMode="linear"
      />
    </circle>

    <!-- 内圈装饰 -->
    <g class="text-secondary-500">
      <circle
        v-for="(dot, index) in dots"
        :key="index"
        :cx="dot.x"
        :cy="dot.y"
        :r="dot.radius"
        fill="currentColor"
      >
        <animate
          attributeName="r"
          :values="`${dot.radius};${dot.radius * 1.5};${dot.radius}`"
          :dur="`${dot.duration}s`"
          repeatCount="indefinite"
          :begin="`${dot.delay}s`"
        />
      </circle>
    </g>

    <!-- 中心图案 -->
    <path
      d="M50 35 L65 55 L35 55 Z"
      class="text-primary-400"
      fill="currentColor"
    >
      <animateTransform
        attributeName="transform"
        type="rotate"
        from="0 50 50"
        to="360 50 50"
        dur="3s"
        repeatCount="indefinite"
      />
    </path>
  </svg>
</template>

<script setup lang="ts">
import { computed, ref } from "vue";

const props = defineProps({
  size: {
    type: Number,
    default: 40,
  },
  spin: {
    type: Boolean,
    default: false,
  },
});

const circumference = computed(() => 2 * Math.PI * 45);
const currentOffset = ref(circumference.value);

// 生成装饰点
const dots = computed(() => {
  const count = 8;
  const radius = 35;
  return Array.from({ length: count }, (_, index) => {
    const angle = (index / count) * Math.PI * 2;
    return {
      x: 50 + Math.cos(angle) * radius,
      y: 50 + Math.sin(angle) * radius,
      radius: 2,
      duration: 1 + Math.random(),
      delay: index * 0.2,
    };
  });
});
</script>

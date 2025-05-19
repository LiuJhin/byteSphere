<template>
  <svg
    class="absolute inset-0 w-full h-full"
    xmlns="http://www.w3.org/2000/svg"
    :viewBox="`0 0 ${width} ${height}`"
  >
    <!-- 动态网格 -->
    <pattern
      id="grid-pattern"
      :width="gridSize"
      :height="gridSize"
      patternUnits="userSpaceOnUse"
    >
      <path
        :d="`M ${gridSize} 0 L 0 0 0 ${gridSize}`"
        fill="none"
        stroke="currentColor"
        stroke-width="0.5"
        class="text-primary-500/10"
      />
    </pattern>
    <rect width="100%" height="100%" fill="url(#grid-pattern)" />

    <!-- 动态光线 -->
    <g v-for="(line, index) in lines" :key="index">
      <line
        :x1="line.x1"
        :y1="line.y1"
        :x2="line.x2"
        :y2="line.y2"
        stroke="currentColor"
        :class="line.color"
        :style="{
          strokeWidth: line.width,
          opacity: line.opacity,
        }"
      >
        <animate
          attributeName="opacity"
          :values="`${line.opacity};0;${line.opacity}`"
          :dur="`${line.duration}s`"
          repeatCount="indefinite"
          :begin="`${line.delay}s`"
        />
      </line>
    </g>

    <!-- 动态点 -->
    <g v-for="(point, index) in points" :key="`point-${index}`">
      <circle
        :cx="point.x"
        :cy="point.y"
        :r="point.radius"
        :class="point.color"
        fill="currentColor"
      >
        <animate
          attributeName="r"
          :values="`${point.radius};${point.radius * 2};${point.radius}`"
          :dur="`${point.duration}s`"
          repeatCount="indefinite"
          :begin="`${point.delay}s`"
        />
        <animate
          attributeName="opacity"
          values="0.8;0.2;0.8"
          :dur="`${point.duration}s`"
          repeatCount="indefinite"
          :begin="`${point.delay}s`"
        />
      </circle>
    </g>
  </svg>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";

const props = defineProps({
  width: {
    type: Number,
    default: 1000,
  },
  height: {
    type: Number,
    default: 1000,
  },
  gridSize: {
    type: Number,
    default: 50,
  },
});

// 生成随机线条
const generateLines = (count: number) => {
  return Array.from({ length: count }, () => ({
    x1: Math.random() * props.width,
    y1: Math.random() * props.height,
    x2: Math.random() * props.width,
    y2: Math.random() * props.height,
    color: Math.random() > 0.5 ? "text-primary-500" : "text-secondary-500",
    width: Math.random() * 2 + 0.5,
    opacity: Math.random() * 0.3 + 0.1,
    duration: Math.random() * 3 + 2,
    delay: Math.random() * 2,
  }));
};

// 生成随机点
const generatePoints = (count: number) => {
  return Array.from({ length: count }, () => ({
    x: Math.random() * props.width,
    y: Math.random() * props.height,
    radius: Math.random() * 3 + 1,
    color: Math.random() > 0.5 ? "text-primary-500" : "text-secondary-500",
    duration: Math.random() * 3 + 2,
    delay: Math.random() * 2,
  }));
};

const lines = ref(generateLines(15));
const points = ref(generatePoints(20));
</script>

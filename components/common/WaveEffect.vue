<template>
  <svg
    class="absolute bottom-0 left-0 w-full"
    xmlns="http://www.w3.org/2000/svg"
    :viewBox="`0 0 ${width} ${height}`"
    preserveAspectRatio="none"
  >
    <!-- 第一层波浪 -->
    <path
      :d="generateWavePath(0)"
      fill="currentColor"
      class="text-primary-500/5"
    >
      <animate
        attributeName="d"
        :values="generateWaveAnimation(0)"
        dur="10s"
        repeatCount="indefinite"
      />
    </path>

    <!-- 第二层波浪 -->
    <path
      :d="generateWavePath(phase2)"
      fill="currentColor"
      class="text-secondary-500/5"
    >
      <animate
        attributeName="d"
        :values="generateWaveAnimation(phase2)"
        dur="8s"
        repeatCount="indefinite"
      />
    </path>

    <!-- 第三层波浪 -->
    <path
      :d="generateWavePath(phase3)"
      fill="currentColor"
      class="text-primary-500/3"
    >
      <animate
        attributeName="d"
        :values="generateWaveAnimation(phase3)"
        dur="6s"
        repeatCount="indefinite"
      />
    </path>
  </svg>
</template>

<script setup lang="ts">
const props = defineProps({
  width: {
    type: Number,
    default: 1440,
  },
  height: {
    type: Number,
    default: 200,
  },
});

const phase2 = Math.PI / 2;
const phase3 = Math.PI;

// 生成波浪路径
const generateWavePath = (phase: number) => {
  const points = [];
  const segments = 20;
  const amplitude = props.height * 0.3;

  for (let i = 0; i <= segments; i++) {
    const x = (i / segments) * props.width;
    const y =
      Math.sin((i / segments) * Math.PI * 2 + phase) * amplitude +
      props.height * 0.5;
    points.push(`${x},${y}`);
  }

  return `M 0,${props.height} L 0,${props.height * 0.5} L ${points.join(
    " L "
  )} L ${props.width},${props.height} Z`;
};

// 生成波浪动画
const generateWaveAnimation = (phase: number) => {
  const frames = 5;
  const paths = [];

  for (let i = 0; i < frames; i++) {
    const framePhase = phase + (i / frames) * Math.PI * 2;
    paths.push(generateWavePath(framePhase));
  }

  return paths.join(";") + ";" + paths[0];
};
</script>

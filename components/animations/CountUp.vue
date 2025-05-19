<template>
  <span>{{ displayValue }}{{ suffix }}</span>
</template>

<script setup lang="ts">
import { ref, onMounted, watch } from "vue";

const props = defineProps<{
  endVal: number;
  duration?: number;
  suffix?: string;
}>();

const displayValue = ref(0);

const animate = () => {
  const start = 0;
  const end = props.endVal;
  const duration = props.duration || 2000;
  const startTime = performance.now();

  const update = () => {
    const currentTime = performance.now();
    const progress = Math.min((currentTime - startTime) / duration, 1);

    displayValue.value = Math.floor(start + (end - start) * progress);

    if (progress < 1) {
      requestAnimationFrame(update);
    }
  };

  requestAnimationFrame(update);
};

onMounted(() => {
  animate();
});

watch(
  () => props.endVal,
  () => {
    animate();
  }
);
</script>

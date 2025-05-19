<template>
  <div ref="el" class="scroll-reveal" :style="styles">
    <slot></slot>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, computed } from "vue";
import { useIntersectionObserver } from "@vueuse/core";

const props = withDefaults(
  defineProps<{
    direction?: "top" | "bottom" | "left" | "right";
    distance?: number;
    delay?: number;
    duration?: number;
  }>(),
  {
    direction: "bottom",
    distance: 50,
    delay: 0,
    duration: 800,
  }
);

const el = ref<HTMLElement | null>(null);
const isVisible = ref(false);

const styles = computed(() => {
  const translateMap = {
    top: `translateY(${isVisible.value ? 0 : props.distance}px)`,
    bottom: `translateY(${isVisible.value ? 0 : -props.distance}px)`,
    left: `translateX(${isVisible.value ? 0 : props.distance}px)`,
    right: `translateX(${isVisible.value ? 0 : -props.distance}px)`,
  };

  return {
    opacity: isVisible.value ? 1 : 0,
    transform: translateMap[props.direction],
    transition: `all ${props.duration}ms cubic-bezier(0.4, 0, 0.2, 1) ${props.delay}ms`,
  };
});

onMounted(() => {
  const { stop } = useIntersectionObserver(
    el,
    ([{ isIntersecting }]) => {
      if (isIntersecting) {
        isVisible.value = true;
        stop();
      }
    },
    { threshold: 0.1 }
  );
});
</script>

<style scoped>
.scroll-reveal {
  opacity: 0;
}
</style>

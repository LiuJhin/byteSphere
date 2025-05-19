<template>
  <div ref="elementRef" class="scroll-reveal">
    <slot></slot>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

const props = defineProps({
  direction: {
    type: String,
    default: "bottom",
    validator: (value: string) =>
      ["left", "right", "top", "bottom"].includes(value),
  },
  distance: {
    type: Number,
    default: 50,
  },
  duration: {
    type: Number,
    default: 1,
  },
  delay: {
    type: Number,
    default: 0,
  },
  stagger: {
    type: Number,
    default: 0.1,
  },
  trigger: {
    type: String,
    default: "80%",
  },
});

const elementRef = ref<HTMLElement | null>(null);

onMounted(() => {
  if (!elementRef.value) return;

  const getInitialPosition = () => {
    switch (props.direction) {
      case "left":
        return { x: -props.distance, y: 0 };
      case "right":
        return { x: props.distance, y: 0 };
      case "top":
        return { x: 0, y: -props.distance };
      case "bottom":
        return { x: 0, y: props.distance };
      default:
        return { x: 0, y: props.distance };
    }
  };

  const elements =
    props.stagger > 0 ? elementRef.value.children : [elementRef.value];

  gsap.from(elements, {
    ...getInitialPosition(),
    opacity: 0,
    duration: props.duration,
    delay: props.delay,
    stagger: props.stagger,
    ease: "power2.out",
    scrollTrigger: {
      trigger: elementRef.value,
      start: `top ${props.trigger}`,
      toggleActions: "play none none reverse",
    },
  });
});
</script>

<style scoped>
.scroll-reveal {
  will-change: transform, opacity;
}
</style>

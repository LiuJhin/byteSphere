<template>
  <svg
    class="absolute inset-0 w-full h-full"
    viewBox="0 0 1000 1000"
    xmlns="http://www.w3.org/2000/svg"
  >
    <defs>
      <linearGradient id="circuit-gradient" x1="0%" y1="0%" x2="100%" y2="100%">
        <stop offset="0%" class="text-primary-500" stop-opacity="0.1" />
        <stop offset="50%" class="text-primary-500" stop-opacity="0.2" />
        <stop offset="100%" class="text-primary-500" stop-opacity="0.1" />
      </linearGradient>

      <filter id="glow">
        <feGaussianBlur stdDeviation="2" result="coloredBlur" />
        <feMerge>
          <feMergeNode in="coloredBlur" />
          <feMergeNode in="SourceGraphic" />
        </feMerge>
      </filter>
    </defs>

    <!-- 电路线路 -->
    <path
      class="circuit-path"
      d="M100,100 L300,100 Q350,100 350,150 L350,300 Q350,350 400,350 L600,350 Q650,350 650,400 L650,600"
      fill="none"
      stroke="url(#circuit-gradient)"
      stroke-width="2"
    />

    <path
      class="circuit-path"
      d="M900,100 L700,100 Q650,100 650,150 L650,250 Q650,300 600,300 L400,300 Q350,300 350,350 L350,500"
      fill="none"
      stroke="url(#circuit-gradient)"
      stroke-width="2"
    />

    <!-- 移动的点 -->
    <circle class="moving-dot" r="4" fill="currentColor" filter="url(#glow)">
      <animateMotion
        dur="3s"
        repeatCount="indefinite"
        path="M100,100 L300,100 Q350,100 350,150 L350,300 Q350,350 400,350 L600,350 Q650,350 650,400 L650,600"
      />
    </circle>

    <circle class="moving-dot" r="4" fill="currentColor" filter="url(#glow)">
      <animateMotion
        dur="4s"
        repeatCount="indefinite"
        path="M900,100 L700,100 Q650,100 650,150 L650,250 Q650,300 600,300 L400,300 Q350,300 350,350 L350,500"
      />
    </circle>
  </svg>
</template>

<style scoped>
.circuit-path {
  stroke-dasharray: 10;
  animation: dash 20s linear infinite;
}

.moving-dot {
  @apply text-primary-400;
}

@keyframes dash {
  to {
    stroke-dashoffset: 1000;
  }
}
</style>

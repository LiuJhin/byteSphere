<template>
  <div class="min-h-screen bg-gray-900 relative">
    <!-- 背景动画 -->
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <div
        class="absolute inset-0 bg-[radial-gradient(circle_at_top_right,rgba(79,70,229,0.1)_0%,transparent_50%)]"
      ></div>
      <CommonCyberGrid class="opacity-10" />
      <div class="absolute top-0 left-0 w-full h-full">
        <svg
          class="animate-float"
          width="100%"
          height="100%"
          viewBox="0 0 100 100"
          preserveAspectRatio="none"
        >
          <defs>
            <linearGradient id="gradient" x1="0%" y1="0%" x2="100%" y2="0%">
              <stop
                offset="0%"
                style="stop-color: rgb(79, 70, 229); stop-opacity: 0.1"
              />
              <stop
                offset="100%"
                style="stop-color: rgb(16, 185, 129); stop-opacity: 0.1"
              />
            </linearGradient>
          </defs>
          <path
            d="M0,50 Q25,30 50,50 T100,50 L100,100 L0,100 Z"
            fill="url(#gradient)"
            class="animate-wave"
          >
            <animate
              attributeName="d"
              dur="5s"
              repeatCount="indefinite"
              values="
                M0,50 Q25,30 50,50 T100,50 L100,100 L0,100 Z;
                M0,50 Q25,70 50,50 T100,50 L100,100 L0,100 Z;
                M0,50 Q25,30 50,50 T100,50 L100,100 L0,100 Z"
            />
          </path>
        </svg>
      </div>
    </div>

    <!-- 顶部导航栏 -->
    <nav
      class="sticky top-0 z-50 backdrop-blur-md bg-gray-900/50 border-b border-gray-800"
    >
      <div
        class="container mx-auto px-4 h-16 flex items-center justify-between"
      >
        <div class="flex items-center space-x-4">
          <button
            @click="router.back()"
            class="group flex items-center space-x-2 text-gray-400 hover:text-white transition-colors"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-5 w-5 transform group-hover:-translate-x-1 transition-transform"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M15 19l-7-7 7-7"
              />
            </svg>
            <span>返回</span>
          </button>
          <div class="h-6 w-px bg-gray-700"></div>
          <h1 class="text-xl font-bold text-white">项目详情</h1>
        </div>
        <div class="flex items-center space-x-2">
          <span class="flex h-3 w-3">
            <span
              class="animate-ping absolute inline-flex h-3 w-3 rounded-full bg-green-400 opacity-75"
            ></span>
            <span
              class="relative inline-flex rounded-full h-3 w-3 bg-green-500"
            ></span>
          </span>
          <span class="text-green-400 text-sm">系统运行中</span>
        </div>
      </div>
    </nav>

    <!-- 主要内容区域 -->
    <div class="container mx-auto px-4 py-8">
      <ScrollReveal>
        <!-- 基本信息卡片 -->
        <div
          class="bg-gray-800/50 backdrop-blur-md rounded-xl border border-gray-700/50 p-6 mb-8 transform hover:scale-[1.02] transition-all duration-300"
        >
          <div class="flex items-start gap-6">
            <div
              class="w-32 h-32 rounded-xl bg-gradient-to-br from-primary-500/20 to-secondary-500/20 flex items-center justify-center group perspective"
            >
              <div
                class="relative w-20 h-20 transform-gpu group-hover:rotate-y-180 transition-transform duration-1000 preserve-3d"
              >
                <div class="absolute inset-0 backface-hidden">
                  <span class="text-5xl">📺</span>
                </div>
                <div class="absolute inset-0 backface-hidden rotate-y-180">
                  <span class="text-5xl">🚀</span>
                </div>
              </div>
            </div>
            <div class="flex-1">
              <div class="flex items-center justify-between mb-4">
                <h2 class="text-3xl font-bold text-white">
                  NikoLive
                  <span
                    class="text-transparent bg-clip-text bg-gradient-to-r from-primary-400 to-secondary-400"
                  >
                    全场景互动直播平台
                  </span>
                </h2>
                <span class="text-gray-400">2024.09 - 至今</span>
              </div>
              <div class="flex items-center gap-4 mb-4">
                <span
                  class="px-3 py-1 rounded-full text-xs font-medium bg-green-500/10 text-green-400 border border-green-500/20"
                >
                  在线运行中
                </span>
                <div class="flex items-center text-gray-400 text-sm">
                  <svg
                    class="w-4 h-4 mr-1"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z"
                    />
                  </svg>
                  日均并发 10万+
                </div>
              </div>
              <p class="text-gray-300 leading-relaxed">
                {{ projectDetail.description }}
              </p>
            </div>
          </div>
        </div>
      </ScrollReveal>

      <ScrollReveal>
        <!-- 技术架构 -->
        <div
          class="bg-gray-800/50 backdrop-blur-md rounded-xl border border-gray-700/50 p-6 mb-8"
        >
          <h3 class="text-2xl font-bold text-white mb-6 flex items-center">
            <span
              class="text-transparent bg-clip-text bg-gradient-to-r from-primary-400 to-secondary-400"
            >
              技术架构
            </span>
            <div
              class="ml-4 flex-1 h-px bg-gradient-to-r from-primary-500/50 to-transparent"
            ></div>
          </h3>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <ScrollReveal
              v-for="(section, index) in architectureSections"
              :key="index"
              :delay="index * 0.1"
            >
              <div
                class="p-4 rounded-lg bg-gray-700/30 hover:bg-gray-700/50 transition-colors group"
              >
                <h4 class="font-semibold text-white mb-2 flex items-center">
                  <span class="text-xl mr-2">{{ section.icon }}</span>
                  {{ section.title }}
                </h4>
                <p class="text-gray-300">{{ section.content }}</p>
              </div>
            </ScrollReveal>
          </div>
        </div>
      </ScrollReveal>

      <!-- 其他部分保持不变，但添加 ScrollReveal 包装 -->
      <ScrollReveal>
        <!-- 核心贡献与技术亮点 -->
        <div
          class="bg-gray-800/50 backdrop-blur-md rounded-xl border border-gray-700/50 p-6 mb-8"
        >
          <h3 class="text-2xl font-bold text-white mb-6 flex items-center">
            <span
              class="text-transparent bg-clip-text bg-gradient-to-r from-primary-400 to-secondary-400"
            >
              核心贡献与技术亮点
            </span>
            <div
              class="ml-4 flex-1 h-px bg-gradient-to-r from-primary-500/50 to-transparent"
            ></div>
          </h3>
          <div class="space-y-6">
            <ScrollReveal
              v-for="(highlight, index) in projectDetail.highlights"
              :key="index"
              :delay="index * 0.1"
              class="transform hover:scale-[1.01] transition-transform duration-300"
            >
              <div
                class="border-l-4 border-primary-500 pl-4 py-2 bg-gray-700/30 rounded-r-lg"
              >
                <h4 class="text-lg font-semibold text-white mb-3">
                  {{ highlight.title }}
                </h4>
                <ul class="space-y-2">
                  <li
                    v-for="(point, idx) in highlight.points"
                    :key="idx"
                    class="text-gray-300 flex items-start"
                  >
                    <span class="text-primary-400 mr-2">•</span>
                    {{ point }}
                  </li>
                </ul>
              </div>
            </ScrollReveal>
          </div>
        </div>
      </ScrollReveal>

      <!-- 创新成果和项目价值部分也类似添加动画效果 -->
      <!-- ... 其他内容保持不变 ... -->
    </div>

    <!-- 底部固定的操作按钮 -->
    <div
      class="fixed bottom-0 left-0 right-0 backdrop-blur-md bg-gray-900/50 border-t border-gray-800"
    >
      <div
        class="container mx-auto px-4 h-16 flex justify-between items-center"
      >
        <div class="flex items-center space-x-6">
          <div class="flex items-center">
            <span class="flex h-3 w-3 relative mr-2">
              <span
                class="animate-ping absolute inline-flex h-full w-full rounded-full bg-green-400 opacity-75"
              ></span>
              <span
                class="relative inline-flex rounded-full h-3 w-3 bg-green-500"
              ></span>
            </span>
            <span class="text-green-400 text-sm">系统在线</span>
          </div>
          <div class="text-gray-300 text-sm">
            日活用户：
            <CountUp :end-val="50" :suffix="'万+'" />
          </div>
        </div>
        <div class="flex gap-4">
          <button class="btn-primary">
            <span class="mr-2">📊</span>
            查看数据面板
          </button>
          <button class="btn-secondary">
            <span class="mr-2">🔗</span>
            访问系统
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { useRouter } from "vue-router";
import ScrollReveal from "~/components/animations/ScrollReveal.vue";
import CommonCyberGrid from "~/components/common/CyberGrid.vue";
import CountUp from "~/components/animations/CountUp.vue";

const router = useRouter();

const architectureSections = [
  {
    icon: "⚛️",
    title: "前端框架",
    content:
      "Vue3 + TypeScript + Pinia状态管理（模块化设计，TS类型覆盖率>90%）",
  },
  {
    icon: "🔄",
    title: "通信层",
    content: "腾讯云TRTC（<300ms超低延迟）+ IM即时通信（信令同步精度<100ms）",
  },
  {
    icon: "🛠️",
    title: "工程化",
    content: "Webpack多环境构建 + Tailwind CSS原子化样式（首屏加载<1.2s）",
  },
  {
    icon: "🚀",
    title: "特色技术",
    content: "WebRTC P2P穿透、VAP动态礼物渲染引擎、混流服务器架构",
  },
];

// 项目详情数据保持不变
const projectDetail = ref({
  description:
    "基于Vue3+TypeScript技术栈构建的综合性直播解决方案，集成低延迟直播、多角色交互、实时连麦PK、动态礼物特效等核心功能，支持横竖屏自适应与多端无缝体验，日均承载10万+并发用户互动。",
  highlights: [
    {
      title: "直播引擎架构设计",
      points: [
        "主导设计多角色直播系统，实现主播/观众角色秒级切换，采用Pinia状态机管理200+直播间事件流，数据同步延迟控制在150ms内",
        "构建TRTC+WebRTC混合推流方案，通过智能路由算法动态切换传输协议，弱网环境下卡顿率降低42%",
        "开发跨房连麦PK系统，支持双主播/多人组队实时混流，采用腾讯云MCU混流服务，音画同步误差<80ms",
      ],
    },
    {
      title: "高并发实时互动系统",
      points: [
        "设计分级消息通道：普通弹幕（WS长连接）、礼物消息（HTTP2+Binary协议）、信令控制（UDP+重试机制）",
        "实现VAP动效礼物体系：开发基于WebGL的渲染引擎，支持粒子特效/3D模型礼物，资源加载效率提升65%",
        "构建实时数据看板：集成ECharts实现秒级更新的在线人数/打赏金额/GMV热力图，数据延迟<500ms",
      ],
    },
    {
      title: "极致性能优化",
      points: [
        "直播流智能降级：根据设备性能动态切换HLS/FLV/WebRTC协议，首帧加载时间优化至0.8s",
        "组件级懒加载：直播间模块按需加载，Webpack分包策略使首包体积减少58%（从3.2MB→1.35MB）",
        "渲染性能提升：采用Tailwind CSS + CSS GPU加速，直播间FPS稳定在60帧，内存占用降低30%",
      ],
    },
    {
      title: "安全与稳定性建设",
      points: [
        "设计动态防盗链体系：推流地址HMAC-SHA256加密 + 时间戳校验，拦截非法请求成功率100%",
        "实现熔断降级机制：当QPS超过阈值时自动切换至备用CDN，系统可用性达99.99%",
        "建立多维度监控：前端Performance API+SentRY异常捕捉，后端TRTC QoS质量巡检",
      ],
    },
  ],
  innovations: [
    {
      icon: "🔄",
      title: "双协议混合推流",
      description:
        "行业首个「双协议混合推流」方案：TRTC保底+WebRTC智能切换，带宽成本降低37%",
    },
    {
      icon: "📱",
      title: "跨端分辨率自适应",
      description:
        "「跨端分辨率自适应」算法：根据设备DPI动态调整推流参数，高清场景码率节约28%",
    },
    {
      icon: "🎁",
      title: "虚拟礼物热更新",
      description:
        "「虚拟礼物热更新」系统：无需发版即可通过CDN动态加载新礼物，功能上线周期缩短70%",
    },
  ],
  values: [
    {
      title: "技术价值",
      content:
        "沉淀直播领域3大核心专利（跨房混流方法、动效渲染引擎、多协议适配架构）",
    },
    {
      title: "业务价值",
      content: "支撑平台上线首月DAU突破50万，主播分成体系带来月均300万流水",
    },
    {
      title: "扩展性",
      content: "架构设计支持快速扩展短视频/语聊房等场景，功能模块复用率达85%",
    },
  ],
});
</script>

<style scoped>
.perspective {
  perspective: 1000px;
}

.preserve-3d {
  transform-style: preserve-3d;
}

.backface-hidden {
  backface-visibility: hidden;
}

.rotate-y-180 {
  transform: rotateY(180deg);
}

.btn-primary {
  @apply px-6 py-2 rounded-full bg-primary-500 text-white hover:bg-primary-600 
    transition-all duration-300 transform hover:scale-105 hover:shadow-lg 
    hover:shadow-primary-500/25 flex items-center;
}

.btn-secondary {
  @apply px-6 py-2 rounded-full bg-gray-700 text-white hover:bg-gray-600 
    transition-all duration-300 transform hover:scale-105 hover:shadow-lg 
    hover:shadow-gray-500/25 flex items-center;
}

.animate-float {
  animation: float 6s ease-in-out infinite;
}

@keyframes float {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
}

.animate-wave {
  animation: wave 5s ease-in-out infinite;
}

@keyframes wave {
  0%,
  100% {
    d: path("M0,50 Q25,30 50,50 T100,50 L100,100 L0,100 Z");
  }
  50% {
    d: path("M0,50 Q25,70 50,50 T100,50 L100,100 L0,100 Z");
  }
}
</style>

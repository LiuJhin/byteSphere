<template>
  <footer class="bg-gray-800 text-gray-300">
    <div class="container mx-auto px-4 py-8">
      <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
        <!-- Company Info -->
        <div>
          <h3 class="text-white text-lg font-semibold mb-4">ByteSphere</h3>
          <p class="text-sm">
            打造最优质的游戏社区平台，为玩家提供极致的游戏体验。
          </p>
        </div>

        <!-- Quick Links -->
        <div>
          <h4 class="text-white text-lg font-semibold mb-4">快速链接</h4>
          <ul class="space-y-2">
            <li v-for="item in quickLinks" :key="item.path">
              <NuxtLink
                :to="item.path"
                class="text-sm hover:text-white transition-colors"
              >
                {{ item.name }}
              </NuxtLink>
            </li>
          </ul>
        </div>

        <!-- Support -->
        <div>
          <h4 class="text-white text-lg font-semibold mb-4">支持</h4>
          <ul class="space-y-2">
            <li v-for="item in supportLinks" :key="item.path">
              <NuxtLink
                :to="item.path"
                class="text-sm hover:text-white transition-colors"
              >
                {{ item.name }}
              </NuxtLink>
            </li>
          </ul>
        </div>

        <!-- Contact -->
        <div>
          <h4 class="text-white text-lg font-semibold mb-4">联系我们</h4>
          <ul class="space-y-2 text-sm">
            <li>邮箱：contact@bytesphere.com</li>
            <li>电话：400-123-4567</li>
            <li>地址：深圳市南山区科技园</li>
          </ul>
        </div>
      </div>

      <!-- Bottom Bar -->
      <div class="border-t border-gray-700 mt-8 pt-8 text-sm text-center">
        <p>&copy; {{ new Date().getFullYear() }} ByteSphere. 保留所有权利。</p>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
const quickLinks = [
  { name: "首页", path: "/" },
  { name: "游戏", path: "/games" },
  { name: "社区", path: "/community" },
  { name: "关于我们", path: "/about" },
];

const supportLinks = [
  { name: "帮助中心", path: "/help" },
  { name: "常见问题", path: "/faq" },
  { name: "用户协议", path: "/terms" },
  { name: "隐私政策", path: "/privacy" },
];
</script>

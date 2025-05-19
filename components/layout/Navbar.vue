<template>
  <nav
    class="bg-gradient-to-r from-gray-900 to-gray-800 fixed w-full top-0 z-50 shadow-lg"
  >
    <div class="container mx-auto px-4">
      <div class="flex items-center justify-between h-16">
        <!-- Logo -->
        <div class="flex-shrink-0 flex items-center space-x-2">
          <div
            class="w-8 h-8 bg-blue-500 rounded-lg flex items-center justify-center"
          >
            <span class="text-white text-xl font-bold">B</span>
          </div>
          <NuxtLink
            to="/"
            class="text-2xl font-bold text-white hover:text-blue-400 transition-colors duration-200"
          >
            ByteSphere
          </NuxtLink>
        </div>

        <!-- Navigation Links -->
        <div class="hidden md:block">
          <div class="flex items-center space-x-1">
            <template v-for="item in navigationItems" :key="item.path">
              <!-- 普通菜单项 -->
              <NuxtLink
                v-if="!item.children"
                :to="item.path"
                class="relative group px-4 py-2 rounded-lg text-gray-300 hover:text-white text-sm font-medium transition-all duration-200 hover:bg-white/10"
                active-class="text-blue-400 bg-white/10"
              >
                <span class="relative z-10 flex items-center">
                  {{ item.name }}
                </span>
                <span
                  class="absolute bottom-0 left-0 w-full h-0.5 bg-blue-500 transform scale-x-0 group-hover:scale-x-100 transition-transform duration-200"
                ></span>
              </NuxtLink>

              <!-- 带下拉菜单的项目 -->
              <div
                v-else
                class="relative group"
                @mouseenter="item.isOpen = true"
                @mouseleave="item.isOpen = false"
              >
                <button
                  class="flex items-center px-4 py-2 rounded-lg text-gray-300 hover:text-white text-sm font-medium transition-all duration-200 hover:bg-white/10"
                  :class="{ 'text-blue-400 bg-white/10': isActiveParent(item) }"
                >
                  <span class="flex items-center gap-2">
                    <!-- 菜单图标 -->
                    <component
                      :is="item.icon || 'div'"
                      class="w-4 h-4"
                      v-if="item.icon"
                    ></component>
                    {{ item.name }}
                  </span>
                  <svg
                    class="w-4 h-4 ml-1 transform transition-transform duration-200"
                    :class="{ 'rotate-180': item.isOpen }"
                    fill="none"
                    viewBox="0 0 24 24"
                    stroke="currentColor"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M19 9l-7 7-7-7"
                    />
                  </svg>
                </button>

                <!-- 下拉菜单 -->
                <Transition
                  enter-active-class="transition duration-100 ease-out"
                  enter-from-class="transform scale-95 opacity-0"
                  enter-to-class="transform scale-100 opacity-100"
                  leave-active-class="transition duration-75 ease-in"
                  leave-from-class="transform scale-100 opacity-100"
                  leave-to-class="transform scale-95 opacity-0"
                >
                  <div
                    v-show="item.isOpen"
                    class="absolute left-0 mt-2 w-56 rounded-xl shadow-lg bg-gray-800/95 backdrop-blur-sm ring-1 ring-black ring-opacity-5 border border-gray-700/50"
                  >
                    <div class="py-2" role="menu">
                      <div
                        v-for="(section, index) in item.children"
                        :key="index"
                      >
                        <!-- 分组标题 -->
                        <div
                          v-if="section.title"
                          class="px-4 py-2 text-xs font-semibold text-gray-400 uppercase tracking-wider"
                        >
                          {{ section.title }}
                        </div>

                        <!-- 分组内容 -->
                        <template
                          v-for="child in section.items || [section]"
                          :key="child.path"
                        >
                          <NuxtLink
                            v-if="!child.separator"
                            :to="child.path"
                            class="group/item flex items-center px-4 py-2 text-sm text-gray-300 hover:text-white hover:bg-white/10"
                            :class="{
                              'border-t border-gray-700/50': child.topBorder,
                              'text-blue-400 bg-white/5': isActivePath(
                                child.path
                              ),
                            }"
                            role="menuitem"
                          >
                            <!-- 子菜单图标 -->
                            <component
                              :is="child.icon || 'div'"
                              class="w-4 h-4 mr-3 text-gray-400 group-hover/item:text-white"
                              v-if="child.icon"
                            ></component>
                            <span class="flex-1">{{ child.name }}</span>
                            <!-- 标签 -->
                            <span
                              v-if="child.badge"
                              class="ml-2 px-2 py-0.5 text-xs font-medium rounded-full"
                              :class="getBadgeClasses(child.badge)"
                            >
                              {{ child.badge.text }}
                            </span>
                            <!-- 快捷键 -->
                            <span
                              v-if="child.shortcut"
                              class="ml-2 text-xs text-gray-400 group-hover/item:text-gray-300"
                            >
                              {{ child.shortcut }}
                            </span>
                          </NuxtLink>
                          <div
                            v-else
                            class="my-2 border-t border-gray-700/50"
                            role="separator"
                          ></div>
                        </template>
                      </div>
                    </div>
                  </div>
                </Transition>
              </div>
            </template>
            <button
              @click="toggleTheme"
              class="p-2 rounded-lg text-gray-300 hover:text-white hover:bg-white/10 transition-colors duration-200"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-5 w-5"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path
                  v-if="isDarkMode"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z"
                />
                <path
                  v-else
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z"
                />
              </svg>
            </button>
          </div>
        </div>

        <!-- Mobile menu button -->
        <div class="md:hidden">
          <button
            @click="isMenuOpen = !isMenuOpen"
            class="p-2 rounded-lg text-gray-400 hover:text-white hover:bg-white/10 transition-colors duration-200 focus:outline-none focus:ring-2 focus:ring-blue-500"
          >
            <span class="sr-only">打开主菜单</span>
            <svg
              class="h-6 w-6"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                v-if="!isMenuOpen"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M4 6h16M4 12h16M4 18h16"
              />
              <path
                v-else
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </button>
        </div>
      </div>

      <!-- Mobile menu -->
      <Transition
        enter-active-class="transition duration-200 ease-out"
        enter-from-class="transform -translate-y-4 opacity-0"
        enter-to-class="transform translate-y-0 opacity-100"
        leave-active-class="transition duration-150 ease-in"
        leave-from-class="transform translate-y-0 opacity-100"
        leave-to-class="transform -translate-y-4 opacity-0"
      >
        <div v-show="isMenuOpen" class="md:hidden">
          <div
            class="px-2 pt-2 pb-3 space-y-1 rounded-lg bg-gray-700/50 backdrop-blur-sm mt-2"
          >
            <template v-for="item in navigationItems" :key="item.path">
              <!-- 普通菜单项 -->
              <NuxtLink
                v-if="!item.children"
                :to="item.path"
                class="block px-3 py-2 rounded-lg text-base font-medium text-gray-300 hover:text-white hover:bg-white/10 transition-colors duration-200"
                active-class="text-blue-400 bg-white/10"
                @click="isMenuOpen = false"
              >
                {{ item.name }}
              </NuxtLink>

              <!-- 带子菜单的项目 -->
              <div v-else class="space-y-1">
                <button
                  @click="item.isOpen = !item.isOpen"
                  class="w-full flex items-center justify-between px-3 py-2 rounded-lg text-base font-medium text-gray-300 hover:text-white hover:bg-white/10 transition-colors duration-200"
                  :class="{ 'text-blue-400 bg-white/10': isActiveParent(item) }"
                >
                  {{ item.name }}
                  <svg
                    class="w-4 h-4 transform transition-transform duration-200"
                    :class="{ 'rotate-180': item.isOpen }"
                    fill="none"
                    viewBox="0 0 24 24"
                    stroke="currentColor"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M19 9l-7 7-7-7"
                    />
                  </svg>
                </button>

                <Transition
                  enter-active-class="transition-all duration-200 ease-out"
                  enter-from-class="max-h-0 opacity-0"
                  enter-to-class="max-h-96 opacity-100"
                  leave-active-class="transition-all duration-200 ease-in"
                  leave-from-class="max-h-96 opacity-100"
                  leave-to-class="max-h-0 opacity-0"
                >
                  <div v-show="item.isOpen" class="pl-4 space-y-1">
                    <NuxtLink
                      v-for="child in item.children"
                      :key="child.path"
                      :to="child.path"
                      class="block px-3 py-2 rounded-lg text-sm font-medium text-gray-300 hover:text-white hover:bg-white/10 transition-colors duration-200"
                      active-class="text-blue-400 bg-white/10"
                      @click="isMenuOpen = false"
                    >
                      {{ child.name }}
                    </NuxtLink>
                  </div>
                </Transition>
              </div>
            </template>

            <button
              @click="toggleTheme"
              class="w-full text-left px-3 py-2 rounded-lg text-base font-medium text-gray-300 hover:text-white hover:bg-white/10 transition-colors duration-200"
            >
              {{ isDarkMode ? "切换到亮色模式" : "切换到暗色模式" }}
            </button>
          </div>
        </div>
      </Transition>
    </div>
  </nav>
</template>

<script setup lang="ts">
import { defineComponent, markRaw } from "vue";

interface Badge {
  text: string;
  type: "success" | "warning" | "info" | "danger";
}

interface MenuItem {
  name: string;
  path: string;
  icon?: any;
  badge?: Badge;
  shortcut?: string;
  topBorder?: boolean;
}

interface MenuSection {
  title: string;
  items: MenuItem[];
}

interface MenuSeparator {
  separator: true;
}

type MenuChild = MenuItem | MenuSection | MenuSeparator;

interface NavigationItem {
  name: string;
  path: string;
  icon?: any;
  isOpen?: boolean;
  children?: MenuChild[];
}

const isMenuOpen = ref(false);
const isDarkMode = ref(true);

// 图标组件
const GameIcon = defineComponent({
  render: () =>
    h(
      "svg",
      {
        xmlns: "http://www.w3.org/2000/svg",
        fill: "none",
        viewBox: "0 0 24 24",
        stroke: "currentColor",
        class: "w-4 h-4",
      },
      [
        h("path", {
          "stroke-linecap": "round",
          "stroke-linejoin": "round",
          "stroke-width": "2",
          d: "M15 5v2m0 4v2m0 4v2M5 5a2 2 0 00-2 2v3a2 2 0 110 4v3a2 2 0 002 2h14a2 2 0 002-2v-3a2 2 0 110-4V7a2 2 0 00-2-2H5z",
        }),
      ]
    ),
});

const CommunityIcon = defineComponent({
  render: () =>
    h(
      "svg",
      {
        xmlns: "http://www.w3.org/2000/svg",
        fill: "none",
        viewBox: "0 0 24 24",
        stroke: "currentColor",
        class: "w-4 h-4",
      },
      [
        h("path", {
          "stroke-linecap": "round",
          "stroke-linejoin": "round",
          "stroke-width": "2",
          d: "M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z",
        }),
      ]
    ),
});

const navigationItems = ref<NavigationItem[]>([
  { name: "首页", path: "/" },
  {
    name: "技术",
    path: "/games",
    isOpen: false,
    icon: GameIcon,
    children: [
      {
        title: "游戏分类",
        items: [
          {
            name: "动作游戏",
            path: "/games/action",
            icon: markRaw(
              defineComponent({
                render: () =>
                  h(
                    "svg",
                    {
                      xmlns: "http://www.w3.org/2000/svg",
                      fill: "none",
                      viewBox: "0 0 24 24",
                      stroke: "currentColor",
                      class: "w-4 h-4",
                    },
                    [
                      h("path", {
                        "stroke-linecap": "round",
                        "stroke-linejoin": "round",
                        "stroke-width": "2",
                        d: "M14.752 11.168l-3.197-2.132A1 1 0 0010 9.87v4.263a1 1 0 001.555.832l3.197-2.132a1 1 0 000-1.664z",
                      }),
                      h("path", {
                        "stroke-linecap": "round",
                        "stroke-linejoin": "round",
                        "stroke-width": "2",
                        d: "M21 12a9 9 0 11-18 0 9 9 0 0118 0z",
                      }),
                    ]
                  ),
              })
            ),
          },
          {
            name: "角色扮演",
            path: "/games/rpg",
            badge: { text: "热门", type: "success" },
          },
          { name: "策略游戏", path: "/games/strategy" },
          { name: "休闲游戏", path: "/games/casual" },
        ],
      },
      { separator: true },
      {
        title: "特色内容",
        items: [
          {
            name: "新品上架",
            path: "/games/new-releases",
            badge: { text: "新", type: "info" },
          },
          {
            name: "特惠游戏",
            path: "/games/deals",
            badge: { text: "促销", type: "warning" },
          },
        ],
      },
    ],
  },
  {
    name: "社区",
    path: "/community",
    isOpen: false,
    icon: CommunityIcon,
    children: [
      {
        name: "讨论区",
        path: "/community/discussions",
        shortcut: "⌘D",
      },
      {
        name: "新闻资讯",
        path: "/community/news",
        badge: { text: "5", type: "info" },
      },
      {
        name: "玩家攻略",
        path: "/community/guides",
        topBorder: true,
      },
    ],
  },
  { name: "关于", path: "/about" },
]);

const toggleTheme = () => {
  isDarkMode.value = !isDarkMode.value;
  // 这里可以添加实际的主题切换逻辑
};

// 检查父菜单项是否处于活动状态
const isActiveParent = (item: NavigationItem) => {
  const route = useRoute();
  if (item.children) {
    return item.children.some((section: MenuChild) => {
      if ("items" in section) {
        return section.items.some((child) => route.path.startsWith(child.path));
      }
      if ("path" in section) {
        return route.path.startsWith(section.path);
      }
      return false;
    });
  }
  return route.path === item.path;
};

// 检查具体路径是否匹配当前路由
const isActivePath = (path: string) => {
  const route = useRoute();
  return route.path === path;
};

// 获取徽章的样式类
const getBadgeClasses = (badge: Badge) => {
  const baseClasses = "inline-flex items-center justify-center";
  const typeClasses = {
    success: "bg-green-500/20 text-green-400",
    warning: "bg-yellow-500/20 text-yellow-400",
    info: "bg-blue-500/20 text-blue-400",
    danger: "bg-red-500/20 text-red-400",
  };
  return `${baseClasses} ${typeClasses[badge.type]}`;
};

// 监听路由变化，关闭移动端菜单
watch(
  () => useRoute().fullPath,
  () => {
    isMenuOpen.value = false;
  }
);
</script>

<template>
  <div class="min-h-screen flex flex-col">
    <LayoutNavbar />
    <main class="flex-grow pt-16">
      <slot />
    </main>
    <LayoutFooter />
  </div>
</template>

<script setup lang="ts">
// 组件会自动导入
</script>

<script setup lang="ts">
const base = import.meta.env.BASE_URL
</script>

<template>
  <div class="h-full flex flex-col pt-6 px-8">
    <div class="flex items-start gap-6">
      <div class="flex-[2]">
        <slot name="title" />
      </div>
      <div class="w-1/4 flex justify-center">
        <img :src="`${base}images/coc-logo-blue.png`" class="h-10 dark:hidden" />
        <img :src="`${base}images/coc-logo-white.png`" class="h-10 hidden dark:block" />
      </div>
    </div>
    <div class="relative flex flex-1 gap-6 mt-6">
      <div class="flex-[2] flex flex-col gap-4">
        <slot name="image" />
      </div>
      <div class="relative w-1/4 self-start border-2 border-slate-300 rounded-2xl p-5 flex flex-col gap-4 text-xs text-gray-800 dark:text-white dark:border-white/30">
        <slot name="content" />
      </div>
    </div>
  </div>
</template>

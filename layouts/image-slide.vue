<script setup lang="ts">
const base = import.meta.env.BASE_URL
defineProps<{ heading: string; subtitle?: string; image: string; notes?: string[] }>()
</script>

<template>
  <div class="slidev-layout default h-full bg-white dark:bg-[#121212]">
    <div class="h-full flex flex-col pt-6 px-8">
      <div class="flex items-start gap-6">
        <div class="flex-[2]">
          <h2 class="text-2xl font-bold leading-none">{{ heading }}</h2>
          <slot name="subtitle">
            <p v-if="subtitle" data-id="subtitle" class="text-base !mt-0 text-slate-500 dark:text-slate-400 w-fit pr-2">
              <AnnotatedText :text="subtitle" />
            </p>
          </slot>
        </div>
        <div class="w-1/4 flex justify-center">
          <img :src="`${base}images/coc-logo-blue.png`" class="h-10 dark:hidden" />
          <img :src="`${base}images/coc-logo-white.png`" class="h-10 hidden dark:block" />
        </div>
      </div>
      <div class="relative flex flex-1 gap-6 mt-6">
        <div class="flex-[2] flex flex-col gap-4">
          <img data-id="svg-image" :src="`${base}${image.replace(/^\//, '')}`" class="w-[80%] h-[80%] object-contain object-left dark:invert" style="color-scheme: light" />
        </div>
        <div data-id="notes-box" class="relative w-1/4 self-start border-2 border-slate-300 rounded-2xl p-5 flex flex-col gap-4 text-xs text-gray-800 dark:text-white dark:border-white/30">
          <ContentList v-if="notes">
            <li v-for="item in notes" :key="item">
              <AnnotatedText :text="item" />
            </li>
          </ContentList>
          <slot v-else name="content" />
        </div>
        <slot name="overlay" />
      </div>
    </div>
  </div>
</template>

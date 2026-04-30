<script setup lang="ts">
import { computed } from 'vue'

defineProps({
  class: { type: String, default: '' },
})
</script>

<template>
  <div
    class="slidev-layout default h-full flex items-center justify-center text-center"
    style="
      background-image: linear-gradient(#0005, #0008), url('/images/coc-background-blue.png');
      background-size: cover;
      background-position: center;
      color: white;
    "
  >
    <img
      src="/images/coc-logo-white.png"
      class="absolute top-4 right-6 h-10 z-10"
    />
    <div class="flex flex-col items-center">
      <slot />
    </div>
  </div>
</template>

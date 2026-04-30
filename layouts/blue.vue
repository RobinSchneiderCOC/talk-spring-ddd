<script setup lang="ts">
import { computed } from 'vue'

defineProps({
  class: { type: String, default: '' },
})

const base = import.meta.env.BASE_URL
const bgStyle = {
  backgroundImage: `linear-gradient(#0005, #0008), url('${base}images/coc-background-blue.png')`,
  backgroundSize: 'cover',
  backgroundPosition: 'center',
  color: 'white',
}
</script>

<template>
  <div
    class="slidev-layout default h-full flex items-center justify-center text-center"
    :style="bgStyle"
  >
    <img
      :src="`${base}images/coc-logo-white.png`"
      class="absolute top-4 right-6 h-10 z-10"
    />
    <div class="flex flex-col items-center">
      <slot />
    </div>
  </div>
</template>

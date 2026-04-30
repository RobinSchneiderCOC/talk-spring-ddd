<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps({
  background: {
    type: String,
    default: undefined,
  },
})

function resolveAssetUrl(url: string) {
  if (url.startsWith('/'))
    return import.meta.env.BASE_URL + url.slice(1)
  return url
}

const style = computed(() => {
  if (!props.background || props.background === 'none') return {}
  const isColor = ['#', 'rgb', 'hsl'].some(v => props.background!.startsWith(v))
  return isColor
    ? { background: props.background }
    : {
        backgroundImage: `linear-gradient(#0005, #0008), url("${resolveAssetUrl(props.background)}")`,
        backgroundRepeat: 'no-repeat',
        backgroundPosition: 'center',
        backgroundSize: 'cover',
        color: 'white',
      }
})
</script>

<template>
  <div class="slidev-layout center h-full grid place-content-center" :style="style">
    <div class="my-auto">
      <slot />
    </div>
  </div>
</template>

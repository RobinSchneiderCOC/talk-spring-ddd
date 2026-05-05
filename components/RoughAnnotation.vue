<script setup lang="ts">
import { annotate } from '@slidev/rough-notation'
import { nextTick, onMounted, onUnmounted, ref, watch } from 'vue'
import { useIsSlideActive, useSlideContext } from '@slidev/client'

const props = withDefaults(defineProps<{
  type?: 'underline' | 'box' | 'circle' | 'highlight' | 'strike-through' | 'crossed-off' | 'bracket'
  color?: string
  strokeWidth?: number
  animationDuration?: number
  delay?: number
  iterations?: number
  multiline?: boolean
  padding?: number | number[]
  opacity?: number
}>(), {
  type: 'underline',
  color: 'darkorange',
  strokeWidth: 4,
  animationDuration: 2000,
  delay: 0,
  iterations: 2,
  multiline: true,
  padding: 2,
  opacity: 1,
})

const el = ref<HTMLElement>()
const isActive = useIsSlideActive()
const { $scale } = useSlideContext()
let annotation: ReturnType<typeof annotate> | null = null

function showAnnotation() {
  if (!el.value) return
  if (annotation) annotation.remove()
  const scale = $scale.value ?? 1
  annotation = annotate(el.value, {
    type: props.type,
    color: props.color,
    strokeWidth: props.strokeWidth * scale,
    animationDuration: props.animationDuration,
    delay: props.delay,
    iterations: props.iterations,
    multiline: props.multiline,
    padding: (Array.isArray(props.padding)
      ? (props.padding as number[]).map(p => p * scale)
      : (props.padding as number) * scale) as number,
    opacity: props.opacity,
  })
  annotation.show()
}

watch(isActive, (active) => {
  if (active) nextTick(showAnnotation)
  else annotation?.hide()
})

onMounted(() => {
  if (isActive.value) showAnnotation()
})

onUnmounted(() => {
  annotation?.remove()
})
</script>

<template>
  <span ref="el" style="display: inline">
    <slot />
  </span>
</template>

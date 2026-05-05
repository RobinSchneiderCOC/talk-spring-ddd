<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps<{ text: string }>()

function linkify(text: string) {
  return text.replace(
    /(https?:\/\/[^\s<]+)/g,
    '<a href="$1" target="_blank" class="opacity-70 break-all">$1</a>'
  )
}

const parts = computed(() => {
  const result: { text: string; marked: boolean; type?: string; delay?: number }[] = []
  const regex = /(__(.+?)(?:\|(\d+))?__)|\(\((.+?)(?:\|(\d+))?\)\)/g
  let last = 0
  let match
  while ((match = regex.exec(props.text)) !== null) {
    if (match.index > last) result.push({ text: props.text.slice(last, match.index), marked: false })
    if (match[1]) {
      // __text|delay__
      result.push({ text: match[2], marked: true, type: 'underline', delay: match[3] ? Number(match[3]) : undefined })
    } else {
      // ((text|delay))
      result.push({ text: match[4], marked: true, type: 'circle', delay: match[5] ? Number(match[5]) : undefined })
    }
    last = match.index + match[0].length
  }
  if (last < props.text.length) result.push({ text: props.text.slice(last), marked: false })
  return result
})
</script>

<template>
  <template v-for="(part, i) in parts" :key="i">
    <RoughAnnotation v-if="part.marked" :type="part.type" :delay="part.delay" :padding="part.type === 'circle' ? [6, 10] : 2">{{ part.text }}</RoughAnnotation>
    <!-- eslint-disable-next-line vue/no-v-html -->
    <span v-else v-html="linkify(part.text)" />
  </template>
</template>

<script setup>
import { useNav } from '@slidev/client'
const { currentPage } = useNav()
</script>

<template>
  <img
    v-if="currentPage !== 4"
    src="/images/coc-logo-white.png"
    class="absolute top-4 right-6 h-10 z-10"
  />
</template>

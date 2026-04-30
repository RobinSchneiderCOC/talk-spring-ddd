<template>
  <div class="slidev-layout default h-full bg-white dark:bg-[#121212]">
    <img
      src="/images/coc-logo-blue.png"
      class="absolute top-4 right-6 h-10 z-10 dark:hidden"
    />
    <img
      src="/images/coc-logo-white.png"
      class="absolute top-4 right-6 h-10 z-10 hidden dark:block"
    />
    <slot />
  </div>
</template>

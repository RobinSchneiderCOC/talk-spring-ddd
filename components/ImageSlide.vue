<template>
  <div class="h-full flex flex-col pt-6 px-8">
    <div>
      <slot name="title" />
    </div>
    <div class="flex flex-1 gap-6 mt-6">
      <div class="flex-[2] flex flex-col gap-4">
        <slot name="image" />
      </div>
      <div class="flex-1 bg-slate-100 rounded-2xl p-5 flex flex-col gap-4 text-sm text-gray-800">
        <slot name="content" />
      </div>
    </div>
  </div>
</template>

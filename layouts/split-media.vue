<script setup>
defineProps({
  bg: { type: String, default: 'var(--brand-ink)' }
})
</script>

<template>
  <div class="grid grid-cols-2 h-full w-full">
    <div class="flex items-center justify-center p-0 overflow-hidden" :style="{ background: bg }">
      <slot name="media" />
    </div>
    <div class="flex flex-col justify-center p-12 gap-4">
      <slot />
    </div>
  </div>
</template>

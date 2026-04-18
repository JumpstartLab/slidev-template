<script setup>
defineProps({
  week: { type: String, required: true },
  title: { type: String, required: true }
})
</script>

<template>
  <div class="flex flex-col h-full">
    <div
      class="text-sm font-mono mb-2 uppercase tracking-widest"
      style="color: var(--brand-accent);"
    >
      {{ week }}
    </div>
    <div
      class="text-3xl font-bold mb-6"
      style="font-family: var(--font-display); color: var(--brand-ink);"
    >
      {{ title }}
    </div>
    <div class="text-lg leading-relaxed space-y-3">
      <slot />
    </div>
  </div>
</template>

<script setup>
defineProps({
  value: { type: String, required: true },
  label: { type: String, default: '' },
  accent: { type: Boolean, default: true }
})
</script>

<template>
  <div class="flex flex-col items-start">
    <div
      class="text-8xl font-bold leading-none"
      :style="{ color: accent ? 'var(--brand-accent)' : 'var(--brand-ink)', fontFamily: 'var(--font-display)' }"
    >
      {{ value }}
    </div>
    <div v-if="label" class="text-lg mt-2 muted">{{ label }}</div>
  </div>
</template>

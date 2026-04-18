<script setup>
defineProps({
  name: { type: String, required: true },
  description: { type: String, required: true },
  number: { type: String, default: '' }
})
</script>

<template>
  <div
    class="flex flex-col p-6 rounded-lg h-full"
    style="background: var(--brand-paper); border: 1px solid var(--brand-rule);"
  >
    <div
      class="text-sm font-mono mb-3"
      style="color: var(--brand-accent); font-family: var(--font-mono);"
    >
      {{ number }}
    </div>
    <div
      class="text-2xl font-bold mb-3"
      style="font-family: var(--font-display); color: var(--brand-ink);"
    >
      {{ name }}
    </div>
    <div class="text-base muted leading-relaxed">
      {{ description }}
    </div>
  </div>
</template>

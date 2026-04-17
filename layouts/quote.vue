<template>
  <div class="slidev-layout dark-slide flex flex-col justify-center items-center p-16 h-full">
    <div class="max-w-4xl text-center">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.slidev-layout :deep(h1) {
  font-size: 3.5rem;
  line-height: 1.15;
}

.slidev-layout :deep(p) {
  font-size: 1.25rem;
  color: var(--brand-muted);
  margin-top: 2rem;
}
</style>

<template>
  <div class="pillar-build">
    <div class="pillar-header">
      <div class="pb-eyebrow">{{ headerEyebrow }}</div>
      <h1 v-html="title" />
    </div>
    <div class="pillar-grid">
      <div
        v-for="(pillar, idx) in pillars"
        :key="idx"
        :class="['pillar-cell', stateFor(idx + 1)]"
      >
        <div class="pillar-num">{{ String(idx + 1).padStart(2, "0") }}</div>
        <div class="pillar-name">{{ pillar }}</div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from "vue";

const props = defineProps({
  pillars: { type: Array, required: true },
  current: { type: [Number, String], default: "all" },
  title: { type: String, default: "" },
  eyebrowPrefix: { type: String, default: "Pillar" },
  summaryEyebrow: { type: String, default: "All" },
});

function stateFor(n) {
  if (props.current === "all") return "active";
  const c = Number(props.current);
  if (n === c) return "active";
  if (n < c) return "past";
  return "future";
}

const headerEyebrow = computed(() => {
  if (props.current === "all") return props.summaryEyebrow;
  return `${props.eyebrowPrefix} ${String(Number(props.current)).padStart(2, "0")}`;
});
</script>

<style scoped>
.pillar-build {
  width: 100%;
}

.pillar-header {
  margin-bottom: 2rem;
}

.pb-eyebrow {
  font-family: var(--font-mono);
  font-size: 0.85rem;
  text-transform: uppercase;
  letter-spacing: 0.18em;
  color: var(--brand-accent-2);
  margin-bottom: 0.85rem;
}

.pillar-header h1 {
  font-family: var(--font-display);
  font-size: 3rem;
  font-weight: 700;
  letter-spacing: -0.02em;
  color: var(--brand-ink);
  line-height: 1.1;
  margin: 0;
}

.pillar-header h1 :deep(em) {
  color: var(--brand-accent);
  font-style: normal;
}

.pillar-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1.5rem 4rem;
  max-width: 850px;
  margin-top: 1rem;
}

.pillar-cell {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  transition: opacity 0.35s ease;
  padding-left: 1rem;
  border-left: 3px solid transparent;
}

.pillar-cell.active {
  border-left-color: var(--brand-accent);
}

.pillar-num {
  font-family: var(--font-mono);
  font-size: 0.85rem;
  letter-spacing: 0.15em;
  color: var(--brand-accent-2);
}

.pillar-name {
  font-family: var(--font-display);
  font-size: 2.4rem;
  font-weight: 700;
  letter-spacing: -0.02em;
  color: var(--brand-ink);
  line-height: 1.1;
}

.pillar-cell.past {
  opacity: 0.4;
}

.pillar-cell.future {
  opacity: 0.18;
}
</style>

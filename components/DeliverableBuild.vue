<template>
  <div class="deliverable-build">
    <div class="del-header">
      <div class="del-eyebrow">{{ headerEyebrow }}</div>
      <h1 v-html="title" />
    </div>
    <div class="del-grid">
      <div
        v-for="(item, idx) in items"
        :key="idx"
        :class="['del-item', stateFor(idx + 1)]"
      >
        <span class="del-num">{{ String(idx + 1).padStart(2, "0") }}</span>
        <span class="del-name">{{ item }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from "vue";

const props = defineProps({
  items: { type: Array, required: true },
  current: { type: [Number, String], default: "all" },
  title: { type: String, default: "" },
  eyebrowPrefix: { type: String, default: "Deliverable" },
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
.deliverable-build {
  width: 100%;
}

.del-header {
  margin-bottom: 1.5rem;
}

.del-eyebrow {
  font-family: var(--font-mono);
  font-size: 0.85rem;
  text-transform: uppercase;
  letter-spacing: 0.18em;
  color: var(--brand-accent-2);
  margin-bottom: 0.85rem;
}

.del-header h1 {
  font-family: var(--font-display);
  font-size: 2.6rem;
  font-weight: 700;
  letter-spacing: -0.02em;
  color: var(--brand-ink);
  line-height: 1.1;
  margin: 0;
}

.del-header h1 :deep(em) {
  color: var(--brand-accent);
  font-style: normal;
}

.del-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-auto-flow: column;
  grid-template-rows: repeat(4, auto);
  gap: 0.85rem 4rem;
  max-width: 1000px;
  margin-top: 0.75rem;
}

.del-item {
  display: flex;
  align-items: baseline;
  gap: 1rem;
  transition: opacity 0.35s ease;
  padding-left: 0.75rem;
  border-left: 3px solid transparent;
}

.del-item.active {
  border-left-color: var(--brand-accent);
}

.del-num {
  font-family: var(--font-mono);
  font-size: 0.95rem;
  color: var(--brand-accent);
  flex-shrink: 0;
  letter-spacing: 0.05em;
}

.del-name {
  font-family: var(--font-display);
  font-size: 1.4rem;
  font-weight: 700;
  letter-spacing: -0.02em;
  color: var(--brand-ink);
  line-height: 1.25;
}

.del-item.past {
  opacity: 0.4;
}

.del-item.future {
  opacity: 0.18;
}
</style>

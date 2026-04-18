<template>
  <div class="bullet-build">
    <div v-if="summaryTitle" class="bullet-header">
      <div class="bb-eyebrow">{{ headerEyebrow }}</div>
      <h1 v-html="summaryTitle" />
    </div>
    <ul>
      <li
        v-for="(bullet, idx) in bullets"
        :key="idx"
        :class="['bullet-item', stateFor(idx + 1)]"
      >
        <span class="bullet-num">{{ String(idx + 1).padStart(2, "0") }}</span>
        <span class="bullet-text">{{ bullet }}</span>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { computed } from "vue";

const props = defineProps({
  bullets: { type: Array, required: true },
  titles: { type: Array, default: () => [] },
  current: { type: [Number, String], default: "all" },
  title: { type: String, default: "" },
  summaryTitle: { type: String, default: "" },
  eyebrow: { type: String, default: "" },
  eyebrowPrefix: { type: String, default: "Step" },
  summaryEyebrow: { type: String, default: "All steps" },
});

function stateFor(n) {
  if (props.current === "all") return "active";
  const c = Number(props.current);
  if (n === c) return "active";
  if (n < c) return "past";
  return "future";
}

const headerEyebrow = computed(() => {
  if (props.eyebrow) return props.eyebrow;
  if (props.current === "all") return props.summaryEyebrow;
  return `${props.eyebrowPrefix} ${String(Number(props.current)).padStart(2, "0")}`;
});

const activeTitle = computed(() => {
  if (props.current === "all") return props.summaryTitle || props.title;
  if (props.titles.length) {
    return props.titles[Number(props.current) - 1] || props.title;
  }
  return props.title;
});

const titleKey = computed(() => String(props.current));
</script>

<style scoped>
.bullet-build {
  width: 100%;
  display: flex;
  flex-direction: column;
}

.bullet-header {
  margin-bottom: 1.5rem;
}

.bb-eyebrow {
  font-family: var(--font-mono);
  font-size: 0.85rem;
  text-transform: uppercase;
  letter-spacing: 0.18em;
  color: var(--brand-accent-2);
  margin-bottom: 0.85rem;
}

.bullet-header h1 {
  font-family: var(--font-display);
  font-size: 2.8rem;
  font-weight: 700;
  letter-spacing: -0.02em;
  color: var(--brand-ink);
  line-height: 1.1;
  margin: 0;
}

.bullet-header h1 :deep(em) {
  color: var(--brand-accent);
  font-style: normal;
}

.title-fade-enter-active,
.title-fade-leave-active {
  transition: opacity 0.25s ease;
}

.title-fade-enter-from,
.title-fade-leave-to {
  opacity: 0;
}

ul {
  list-style: none;
  padding: 0;
  margin: 1rem 0 0;
  display: flex;
  flex-direction: column;
  gap: 0.85rem;
}

.bullet-item {
  display: flex;
  align-items: baseline;
  gap: 1rem;
  transition: opacity 0.35s ease;
  padding-left: 0.75rem;
  border-left: 3px solid transparent;
}

.bullet-item.active {
  border-left-color: var(--brand-accent);
}

.bullet-num {
  font-family: var(--font-mono);
  font-size: 0.95rem;
  color: var(--brand-accent);
  flex-shrink: 0;
  letter-spacing: 0.05em;
}

.bullet-text {
  font-family: var(--font-display);
  font-size: 1.5rem;
  font-weight: 600;
  letter-spacing: -0.01em;
  color: var(--brand-ink);
  line-height: 1.3;
}

.bullet-item.past {
  opacity: 0.4;
}

.bullet-item.future {
  opacity: 0.18;
}
</style>

<template>
  <div class="outcome-build">
    <div class="outcome-header">
      <div class="ob-eyebrow">{{ eyebrow }}</div>
      <h1 v-if="arcLine1Html || arcLine2Html" class="arc-title">
        <span v-if="arcLine1Html" class="arc-line arc-line-1" v-html="arcLine1Html" />
        <span v-if="arcLine2Html" class="arc-line arc-line-2" v-html="arcLine2Html" />
      </h1>
      <h1 v-else-if="titleHtml" v-html="titleHtml" />
    </div>
    <div :class="['outcome-grid', `rows-${rows}`]">
      <div
        v-for="(outcome, idx) in outcomes"
        :key="idx"
        :class="['outcome-item', stateFor(idx + 1)]"
      >
        <div class="outcome-num">{{ String(idx + 1).padStart(2, "0") }}</div>
        <div class="outcome-name">{{ typeof outcome === 'string' ? outcome : outcome.name }}</div>
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  outcomes: { type: Array, required: true },
  current: { type: [Number, String], default: "all" },
  eyebrow: { type: String, default: "Outcomes" },
  titleHtml: { type: String, default: "" },
  arcLine1Html: { type: String, default: "" },
  arcLine2Html: { type: String, default: "" },
  rows: { type: Number, default: 3 },
});

function stateFor(n) {
  if (props.current === "all") return "active";
  const c = Number(props.current);
  if (n === c) return "active";
  if (n < c) return "past";
  return "future";
}
</script>

<style scoped>
.outcome-build {
  width: 100%;
  display: flex;
  flex-direction: column;
}

.outcome-header {
  margin-bottom: 1.5rem;
}

.ob-eyebrow {
  font-family: var(--font-mono);
  font-size: 0.85rem;
  text-transform: uppercase;
  letter-spacing: 0.18em;
  color: var(--brand-accent-2);
  margin-bottom: 0.85rem;
}

.outcome-header h1 {
  font-family: var(--font-display);
  font-size: 3rem;
  font-weight: 700;
  letter-spacing: -0.02em;
  color: var(--brand-ink);
  line-height: 1.1;
  margin: 0;
}

.outcome-header h1 :deep(em) {
  color: var(--brand-accent);
  font-style: normal;
}

.arc-title {
  position: relative;
  display: flex;
  flex-direction: column;
  gap: 0.1em;
}

.arc-line-2 {
  text-align: right;
}

.outcome-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-auto-flow: column;
  gap: 1.1rem 4rem;
  max-width: 1000px;
  margin: 1rem 0 0;
}

.outcome-grid.rows-2 { grid-template-rows: repeat(2, auto); }
.outcome-grid.rows-3 { grid-template-rows: repeat(3, auto); }
.outcome-grid.rows-4 { grid-template-rows: repeat(4, auto); }
.outcome-grid.rows-5 { grid-template-rows: repeat(5, auto); }

.outcome-item {
  display: flex;
  align-items: baseline;
  gap: 1rem;
  transition: opacity 0.35s ease;
  padding-left: 0.75rem;
  border-left: 3px solid transparent;
}

.outcome-item.active {
  border-left-color: var(--brand-accent);
}

.outcome-num {
  font-family: var(--font-mono);
  font-size: 0.95rem;
  color: var(--brand-accent);
  flex-shrink: 0;
  letter-spacing: 0.05em;
}

.outcome-name {
  font-family: var(--font-display);
  font-size: 1.4rem;
  font-weight: 700;
  letter-spacing: -0.02em;
  color: var(--brand-ink);
  line-height: 1.25;
}

.outcome-item.past {
  opacity: 0.4;
}

.outcome-item.future {
  opacity: 0.18;
}
</style>

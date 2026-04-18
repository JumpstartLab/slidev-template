# Template Learnings

Patterns, conventions, and gotchas that have compounded into the template from shipped decks. When adding to this file, lead with the pattern, then show the shape, then explain when to reach for it.

---

## The progressive-reveal component pattern

All build components (`BulletBuild`, `PillarBuild`, `DeliverableBuild`, `OutcomeBuild`) share one API convention: a `current` prop that accepts either a 1-based index or the literal string `"all"`. Items before `current` get the `past` state (40% opacity), the current item is `active` (100%, accented border), items after are `future` (18% opacity).

**Why this matters:** a deck that uses the same reveal API across components reads as coherent. A deck that invents a new reveal pattern per component reads as sloppy. When adding a new build component, match this API — don't invent a new one.

**Shape:**

```vue
<PillarBuild
  :pillars="['Discovery', 'Design', 'Build', 'Ship']"
  :current="2"
  title="Our <em>four</em> pillars"
/>
```

`current="1"` through `current="N"` for progressive slides, `current="all"` for the summary slide that reveals everything.

---

## The eyebrow + display headline + accent-`<em>` convention

Every section-header slide uses three parts:

1. **Eyebrow** — small-caps mono label in `var(--brand-accent-2)`, describes the section or step.
2. **Display headline** — large `var(--font-display)` text, the slide's thesis as a sentence.
3. **`<em>` for emphasis** — italics are rendered non-italic but in `var(--brand-accent)`. Use `<em>` to mark the word or phrase the slide lands on.

```html
<div class="eyebrow">Deliverable 03</div>
<h1>Ship the <em>brief</em>.</h1>
```

**Why this matters:** the eyebrow orients the audience, the headline delivers the payload, the `<em>` is where the eye lands. Skipping the eyebrow or flattening the em color breaks the rhythm.

---

## Color tokens, never colors

Every component uses `var(--brand-*)` CSS custom properties. A deck can rebrand entirely by editing `style.css`'s `:root` block — no component edits required.

**The palette:**

| Token | Default (light) | Role |
|---|---|---|
| `--brand-ink` | slate-900 | Primary text, strongest emphasis |
| `--brand-ink-strong` | slate-700 | Secondary emphasis, de-emphasized headings |
| `--brand-muted-strong` | slate-600 | Body text on dark backgrounds, subheadings |
| `--brand-muted` | slate-500 | Secondary text, labels |
| `--brand-accent` | orange-500 | Primary emphasis, `<em>` text, active borders |
| `--brand-accent-2` | cyan-600 | Eyebrows, numbers, secondary emphasis |
| `--brand-accent-soft` | orange-200 | Highlight washes |
| `--brand-rule` | slate-200 | Dividers |

**Why this matters:** client decks fork the template, change the palette, and inherit every pattern untouched. The moment a component hardcodes a color, that rebrandability breaks.

---

## The slides-export escape hatch

`.gitignore` excludes `slides-export/` and `slides-export.pdf` because `slidev export` drops artifacts there and they shouldn't pollute version control. `playwright-chromium` is a devDep because slidev's PDF export requires it.

---

## Retrospectives go upstream

Every deck that ships runs the `deck` orchestrator's compound phase, which diffs the deck against the template at fork time and proposes a PR back here. That's how this file grows. If you find yourself building the same component in two decks, that's a signal to extract it.

**Rule of three:** client-specific once. Suspicious twice. Extract on three.

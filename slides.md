---
theme: seriph
title: Deck Title Goes Here
author: Jeff Casimir
info: |
  Template demo — replace this content for each new deck.
transition: slide-left
mdc: true
fonts:
  sans: Inter
  serif: Inter Tight
  mono: JetBrains Mono
---

# _Deck_ Title Goes Here

<hr class="accent-rule" />

A short positioning line — what this deck is about, in one breath.

<div class="muted mt-12">
  Jeff Casimir · {{ new Date().toLocaleDateString() }}
</div>

---
layout: quote
---

# A punch line that sets the thesis.

One follow-up sentence that expands it just enough.

---
transition: slide-up
---

# The _Problem_

<v-clicks>

- The first thing that's going wrong
- The second thing, which makes the first worse
- The third thing, which nobody wants to say out loud

</v-clicks>

---

# By the _Numbers_

<div class="grid grid-cols-3 gap-8 mt-12">
  <BigStat value="85/50" label="session quality variance" />
  <BigStat value="~20" label="instructors who've run a workshop" />
  <BigStat value="8-12" label="stable core we're aiming for" />
</div>

---
layout: split-media
---

::media::

<img src="https://placehold.co/800x1000/0f172a/f97316?text=Visual" class="h-full w-full object-cover" />

::default::

# The _Shape_ of the Fix

<v-clicks>

- Three session archetypes
- A pre-flight checklist per archetype
- A post-class feedback loop
- A live pilot that proves the delta

</v-clicks>

---

# A _Code_ Moment

```ts {1|3-4|6|all}
const session = await recruit.instructor(topic)

await session.prep(checklist)   // what changes
await session.teach(archetype)  // without flattening voice

return session.feedback()       // signal, not noise
```

---
transition: fade
---

# Embedded _Video_ Example

<div class="flex justify-center mt-8">
  <Youtube id="dQw4w9WgXcQ" width="720" height="405" />
</div>

<div class="muted text-sm text-center mt-4">
  Replace the id above with a real video when authoring
</div>

---
layout: quote
---

# The _close_ — what you want them to walk away carrying.

One sentence of next-step, or a single CTA.

---
layout: center
class: text-center
---

# Thanks

<hr class="accent-rule" style="margin-left: auto; margin-right: auto;" />

<div class="muted">
  jeff@example.com · links · whatever you'd put here
</div>

# slidev-template

Personal Slidev starter. Clone for each new deck; edit in place.

## Make a new deck

```bash
git clone ~/Projects/slidev-template ~/Projects/<deck-name>
cd ~/Projects/<deck-name>
rm -rf .git && git init
npm install
npm run dev
```

Or skip git:

```bash
cp -R ~/Projects/slidev-template ~/Projects/<deck-name>
cd ~/Projects/<deck-name>
npm install
npm run dev
```

Dev server opens the deck at `http://localhost:3030`. Edits to `slides.md` hot-reload.

## What's in here

- `slides.md` — the deck. Starter content demonstrates every pattern below.
- `style.css` — brand tokens (colors, fonts) as CSS custom properties. Change these, every slide updates.
- `layouts/` — custom layouts. `split-media.vue` (two-column with media slot), `quote.vue` (dark centered hero). Reference in frontmatter with `layout: split-media`.
- `components/` — reusable Vue components auto-registered on every slide. `BigStat.vue` for hero numbers. See `components/README.md` for props.
- `global-bottom.vue` — persistent overlay at bottom of every slide (author name from frontmatter).
- `public/` — static assets (images, videos). Reference with absolute paths: `/myimage.png`.
- `snippets/` — reusable code snippets importable into slides.

## The visual-pop techniques

All demonstrated in `slides.md`:

- **Slide transitions** — `transition: slide-left | slide-up | fade` in slide frontmatter
- **Progressive disclosure** — wrap bullets in `<v-clicks>` for click-to-reveal
- **Element animation** — `v-motion :initial="..." :enter="..."` for entrance effects
- **Line-by-line code reveal** — ` ```ts {1|3-4|all} ` syntax highlights different lines on each click
- **Custom layouts** — `layout: split-media` with `::media::` and `::default::` slots
- **Embedded video** — `<Youtube id="..." />` or `<SlidevVideo src="/demo.mp4" />` components
- **Big numbers** — `<BigStat value="85/50" label="..." />` for hero metrics

## Export

```bash
npm run export      # PDF (requires Playwright; auto-installs on first run)
npm run export-png  # PNG per slide
npm run build       # static SPA in dist/ — deploy anywhere
```

## Recording video

Slidev has built-in screen + camera recording in the presenter UI. From the running dev server, click the record icon in the navbar. Exports to WebM.

For voiceover-over-slides (e.g., proposal videos), use the presenter view, hit record, advance through slides while talking.

## Brand customization

Edit `style.css` — change the `--brand-*` custom properties at the top. That's the only file you need to touch for colors, fonts, accent treatments. Everything else references those tokens.

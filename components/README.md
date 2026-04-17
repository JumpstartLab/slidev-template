# Components

Auto-registered Vue components available on every slide. When adding a component, list it here with its props — this is Claude's reference for reusing them cleanly.

## BigStat

Large emphatic number with an optional label. Use for surfacing a single hero metric.

Props:
- `value` (string, required) — the number/text to display large
- `label` (string, optional) — small caption below the number
- `accent` (boolean, default `true`) — when true, number uses `--brand-accent`; when false, uses `--brand-ink`

Example:
```html
<BigStat value="85/50" label="current session quality variance" />
```

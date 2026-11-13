# Brand

Built on the shadcn preset `b1uGaJrhQ` (style Rhea, base Stone, theme Cyan, Tabler icons, small radius). The exact values live in `frontend/src/index.css`; use its tokens, never raw colors.

## Fonts

From Google Fonts:

- **Headings and body**: Instrument Sans
- **Numbers, tables, tickers and citations**: JetBrains Mono, with tabular figures

## Colors

- **Primary**: Cyan (`primary`), for buttons and the brand
- **Citations and links**: `citation`, cyan, lighter in dark mode so it stays readable
- **Increase**: `positive`, green
- **Decrease or error**: `negative`, red
- **Not disclosed or warning**: `warning`, amber
- **Neutrals**: Stone (`background`, `card`, `muted`, `border`)
- **Charts**: `chart-1` to `chart-5`: teal, navy, amber, purple, gray. Use them in that order for peer series.

## Surfaces

- Light and dark mode from `prefers-color-scheme`.
- Two panes: chat on the left, cited sources on the right.
- Cards are rounded with no outline.

## Numbers

- Units always shown: $1,250.0M, 42.3%, FY2025, Q3 FY2026.
- Negatives in parentheses and red: ($84.2M). Never color alone; changes carry a sign.
- Each claim ends with a citation chip, such as `AMD 10-K 2025 · Item 7`.

## Avoid

- Borders on one edge of a panel, and thin lines across the top of the page
- Gradients, shadows and emojis
- Cyan `primary` as text in dark mode; use `citation` instead

## Tone

Plain business English in US spelling, like an analyst's note. Short labels, no jargon, no exclamation marks, no investment advice.
# MineralRightsForum Redesign — Design Tokens

**Canonical design language for all MRF-adjacent work.**

---

## Colors

| Token | Hex | RGB | Use | Notes |
|---|---|---|---|---|
| Navy | `#0a192f` | 10, 25, 47 | Primary background, header, text | Dark navy base |
| Navy Mid | `#0e2040` | 14, 32, 64 | Card gradients, dark panels | Slightly lighter |
| Navy Light | `#1a3054` | 26, 48, 84 | Hover states, focus rings | Interactive layer |
| Gold | `#c5a059` | 197, 160, 89 | Accents, CTAs, links, active states | Primary accent |
| Gold Hover | `#d4b06a` | 212, 176, 106 | Interactive hover, active links | Brightened for interaction |
| Gold Dim | `rgba(197, 160, 89, 0.10)` | — | Badge backgrounds, subtle fills | 10% opacity |
| Gold Border | `rgba(197, 160, 89, 0.25)` | — | Subtle borders on dark backgrounds | 25% opacity |
| Off-white | `#f8f6f1` | 248, 246, 241 | Page background, light text on dark | Warm neutral |
| Ink | `#0b0e14` | 11, 14, 20 | Body text on light backgrounds | Nearly black |
| Muted | `#6b7280` | 107, 114, 128 | Secondary text, meta, labels | Neutral gray |
| Border | `#e6e7ea` | 230, 231, 234 | Dividers, subtle lines | Light gray |

---

## Typography

### Font Families
- **Headings**: Playfair Display (serif) — Google Fonts
- **Body/UI**: Inter (sans-serif) — Google Fonts

### Font Scale

| Role | Font | Weight | Size | Line Height | Notes |
|---|---|---|---|---|---|
| Display / Hero | Playfair Display | 700 | `clamp(2rem, 4vw, 3.25rem)` | 1.2 | Responsive scaling |
| Section Headings | Playfair Display | 700 | 1.75rem–2.5rem | 1.3 | Category/topic section |
| Card Headings | Playfair Display | 700 | 1.125rem–1.375rem | 1.3 | Topic titles |
| Body Copy | Inter | 400 | 1rem | 1.65 | Main post content |
| Eyebrow Labels | Inter | 600 | 0.6875rem | 1.4 | `text-transform: uppercase; letter-spacing: 0.22em` |
| UI / Topic Titles | Inter | 600 | 0.9375rem | 1.4 | Navigation, buttons |
| Meta / Timestamps | Inter | 500 | 0.8125rem | 1.4 | Byline, post date |

### Google Fonts Import
```html
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;0,700;1,400;1,700&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

---

## Component Styles

### Buttons
- **Primary**: Gold background, navy text, 600 weight, border-radius 3px
- **Hover**: Brighter gold (`#d4b06a`), same navy text
- **Disabled**: Gold Dim background, muted text

### Links
- **Default**: Gold text
- **Hover**: Brighter gold with subtle underline
- **Active**: Gold with navy background

### Borders
- **Header Border**: 3px solid gold (bottom)
- **Footer Border**: 3px solid gold (top)
- **Card Borders**: 1px solid border gray
- **Interactive Borders**: 1px solid gold border on hover/focus

### Spacing
- Base unit: `1rem` (16px)
- Header padding: `1.5rem` vertical
- Card padding: `1.5rem` / `1rem` (desktop/mobile)
- Section margin: `3rem` top/bottom

---

## Accessibility Notes

- Navy + Gold has sufficient contrast for WCAG AA compliance
- Off-white backgrounds with navy text meet WCAG AAA
- Always provide focus rings (use navy light or gold border)
- Ensure hover and active states are distinct

---

## Usage in Discourse

See `stylesheets/desktop.scss` and `stylesheets/mobile.scss` for implementation in the theme component.

CSS variables available in Discourse:
```css
--primary: #0a192f
--secondary: #ffffff
--tertiary: #c5a059
--header_background: #0a192f
--header_primary: #ffffff
--highlight: #c5a059
```

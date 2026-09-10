# Design System Inspired by Coinbase

## 1. Visual Theme & Atmosphere

Coinbase's interface solves a hard problem: make raw financial numbers feel
safe. The site is built on an almost clinical white canvas — no photography,
no hero video, no atmospheric imagery — because the product itself (prices,
charts, balances) is the content. Trust is manufactured through restraint:
generous whitespace, a single confident blue, soft rounded corners, and a
neutral gray type hierarchy that never shouts. Where Tesla uses photography
to carry emotional weight, Coinbase uses *cleanliness* — every card, table
row, and button looks like it was designed by someone who understands that
people are looking at numbers that affect their money, and any visual noise
reads as risk.

This maps directly onto this project: `index.html`/`stock-*.html` are not a
product showroom, they're a scanning tool that tells a stranger "here is a
buy signal, here is why, here is the risk." The Coinbase language — soft
cards on a white/near-white ground, one blue accent, semantic green/red for
gains and losses, no drama — communicates "this is a serious data tool, not
a hype page," which is exactly the credibility this dashboard needs given
the mandatory disclaimer language already used across pages ("투자 판단은
본인 책임입니다").

**Key Characteristics:**
- Pure white / near-white page background — content and cards provide all structure
- Soft, friendly rounding (12–16px) on cards, vs. sharp 4px Tesla buttons — approachable, not austere
- Single confident blue accent (`#0052FF`) for primary actions and links, used sparingly
- Semantic red/green reserved exclusively for price/percentage movement — never decorative
- Subtle card elevation (soft shadow or 1px hairline border) instead of Tesla's pure flatness — cards need to read as distinct "modules" of data
- Numeric data set in tabular/monospaced-feel alignment so columns of prices/percentages scan cleanly
- Calm, low-drama motion — 0.15–0.2s ease transitions, no scale/bounce effects
- Dense information tolerated, but always inside a card or table row — never floating loose on the page

## 2. Color Palette & Roles

### Primary
- **Coinbase Blue** (`#0052FF`): Primary CTA background, active nav state, links, and focus rings — the one chromatic anchor of the system (rgb 0, 82, 255)
- **Pure White** (`#FFFFFF`): Primary page and card background

### Secondary & Accent
- **Blue Tint** (`#EAF0FF`): Light blue background for selected states, info callouts, hover backgrounds on nav/menu items
- **Blue Hover** (`#0040CC`): Darkened blue for button/link hover and active-press states

### Surface & Background
- **Page Ground** (`#F7F8FA`): Very light neutral gray used behind card grids and table zones so white cards visibly separate from the page
- **Card Surface** (`#FFFFFF`): All cards, table containers, modals
- **Hairline Surface** (`#F0F1F3`): Alternating table row background / subtle section dividers

### Neutrals & Text
- **Ink** (`#0A0B0D`): Headings, primary numeric values (prices, tickers) — near-black, not pure black
- **Slate** (`#5B616E`): Body copy, descriptions, card subtext
- **Steel** (`#8A919E`): Metadata, timestamps, secondary labels ("시총 상위 100종목 · 매시간")
- **Fog** (`#C3C7CF`): Disabled text, placeholder text, chevron/arrow icons
- **Border Hairline** (`#E3E6EA`): 1px card borders and table cell dividers

### Semantic (critical for this project — stock data)
- **Gain Green** (`#05B169`): Positive price change, "buy signal triggered," bullish badges
- **Gain Green Tint** (`#E6F9EF`): Background for positive-change table cells/badges
- **Loss Red** (`#DF1B41`): Negative price change, bearish/warning badges, disclaimer icon accent
- **Loss Red Tint** (`#FCE9EC`): Background for negative-change table cells/badges
- **Caution Amber** (`#F4A81E`): "셋업 감지, 아직 미확정" / pending-state badges (W패턴 SETUP vs BREAKOUT)
- Semantic colors are used **only** for directional financial meaning — never as decoration. A green badge always means "up/positive," never "success" in a generic UI sense

### Gradient System
- No gradients on structural surfaces (cards, nav, backgrounds stay flat)
- The only permitted gradient is a very subtle 1–2% white-to-`#FAFBFC` wash behind full-width hero/summary bands, meant to be nearly imperceptible — never a visible color gradient

## 3. Typography Rules

### Font Family
- **UI/Body**: `-apple-system, BlinkMacSystemFont, "Segoe UI", "Apple SD Gothic Neo", "Malgun Gothic", "Hiragino Sans", Arial, sans-serif` — system font stack (no custom webfont load) to keep the static pages fast and to render Korean/Japanese/English correctly without a webfont dependency
- **Numeric/Tabular data**: same stack, but numeric columns (price, %, RSI, volume) use `font-variant-numeric: tabular-nums` so digits align vertically in tables
- No serif anywhere; no monospace except where explicitly noted for numeric alignment

### Hierarchy

| Role | Size | Weight | Line Height | Notes |
|------|------|--------|-------------|-------|
| Page Title (H1) | 22–24px | 600 | 1.3 | Hub/guide page titles, Ink color |
| Section Title (H2) | 17–18px | 600 | 1.3 | Card headings ("AND 신호 스캔") |
| Ticker/Price (large) | 20–28px | 600 | 1.2 | Tabular-nums, Ink color |
| Body Text | 13–14px | 400 | 1.6 | Card descriptions, guide copy |
| Metadata/Caption | 11.5–12px | 500 | 1.5 | Timestamps, scan cadence, Steel color |
| Badge/Label | 12px | 600 | 1.2 | Signal badges (BREAKOUT, SETUP), uppercase optional |
| Button Label | 14px | 600 | 1.2 | CTA text |
| Table Header | 12px | 600 | 1.4 | Uppercase, Steel color, letter-spacing +0.02em |

### Principles
- **Weight carries hierarchy, not size**: 600 for anything the eye should land on first (titles, prices, CTAs), 400 for everything read at leisure (descriptions)
- **Slight negative tracking on headings only** (-0.01em), body text stays at normal tracking for readability across three languages
- **Numeric columns are tabular**: any RSI/price/volume/percentage table must use tabular-nums so vertical scanning works — this is a correctness requirement for a scan-result table, not a style preference
- **No uppercase for body/headings**: reserve uppercase strictly for small badges and table headers, matching Coinbase's restrained use of caps
- **Line-height stays generous (1.5–1.6) on body copy** even at small sizes, since guide/disclaimer text is read carefully, not skimmed

## 4. Component Stylings

### Buttons
Rounded, friendly geometry — a deliberate contrast to Tesla's 4px sharpness.

**Primary CTA**:
- bg `#0052FF`, text `#FFFFFF`, fontSize 14px, fontWeight 600, borderRadius 8px, padding 10px 20px, minHeight 40px
- Hover: bg `#0040CC`; Active: bg `#0040CC` + scale unchanged (no transform, color-only)
- Transition: `background-color 0.15s ease`
- Used for: primary navigation actions ("전체 대시보드 바로가기"), simulator "계산하기" button

**Secondary Button**:
- bg `#FFFFFF`, text `#0052FF`, border `1px solid #E3E6EA`, same radius/padding as primary
- Hover: bg `#EAF0FF`, border color `#0052FF`

**Ghost/Text Link**:
- text `#0052FF`, no background, no border, underline on hover only
- Used inline within body copy and card arrows ("›")

### Cards & Containers
The dominant structural pattern of this entire project (hub cards, stock detail cards, guide sections).

- Background: `#FFFFFF`
- Border: `1px solid #E3E6EA` (hairline, always present — replaces Tesla's borderless philosophy since cards must read as distinct data modules)
- Border radius: 12–16px
- Shadow: `0 1px 2px rgba(10,11,13,0.04)` at rest; `0 2px 8px rgba(10,11,13,0.08)` on hover for clickable cards
- Padding: 18–20px
- Transition: `background-color 0.15s ease, box-shadow 0.15s ease` (no transform/scale)
- Clickable card (e.g. hub `.card` linking to a scan table) additionally shows a trailing chevron (Steel color) and a barely-perceptible background shift on `:active`

### Signal Badges
New component vocabulary needed for this project (not present in Tesla's system):
- Pill shape, borderRadius 999px, padding 4px 10px, fontSize 12px, fontWeight 600
- **Breakout/Buy**: bg `#E6F9EF`, text `#05B169`
- **Setup/Pending**: bg `#FEF6E7`, text `#F4A81E`
- **No signal / neutral**: bg `#F0F1F3`, text `#5B616E`
- Never filled solid — always tint-background + saturated text, matching Coinbase's badge convention

### Data Tables (`sp500_table.html`, `wpattern_table.html`)
- Header row: bg `#F7F8FA`, text `#5B616E`, fontWeight 600, fontSize 12px, uppercase, sticky on scroll
- Body rows: bg `#FFFFFF`, alternating `#FAFBFC` for zebra striping on wide tables
- Row border: `1px solid #F0F1F3` (bottom only, no vertical rules)
- Row hover: bg `#EAF0FF` (very subtle, signals "this row is scannable/clickable" if linked)
- Numeric cells: right-aligned, tabular-nums, colored `#05B169`/`#DF1B41` when representing signed change
- Cell padding: 10px 12px minimum for touch/scan comfort on mobile

### Inputs & Forms (dividend simulator)
- Background: `#FFFFFF`, border `1px solid #E3E6EA`, borderRadius 8px, padding 10px 12px
- Focus: border `#0052FF`, box-shadow `0 0 0 3px rgba(0,82,255,0.12)` (soft focus ring, replaces Tesla's border-based focus)
- Label: 12px, fontWeight 600, `#5B616E`, positioned above field
- Placeholder: `#C3C7CF`

### Disclaimer / Callout Box
Already present across pages ("⚠️ 투자 판단은 본인 책임입니다") — formalize as a component:
- bg `#F7F8FA` (neutral) or `#FEF6E7` (amber, when warning-toned)
- borderRadius 12px, padding 12px 14px, fontSize 12.5px, fontWeight 500
- Icon + text in flex row, gap 8px, icon does not get a colored background

### Navigation
- White background, `1px solid #E3E6EA` bottom border (Coinbase always keeps a hairline separator, unlike Tesla's borderless float)
- No frosted-glass/backdrop-filter — flat white at all scroll positions
- Active nav item: text `#0052FF`, optional `#EAF0FF` pill background

## 5. Layout Principles

### Spacing System
- **Base unit**: 4px (finer-grained than Tesla's 8px, needed for dense numeric tables)
- **Common values**: 4, 8, 12, 16, 20, 24, 32px
- **Card gap**: 12–14px between stacked cards (hub page), 16px in grid layouts
- **Section spacing**: 32–40px between major page sections (not full-viewport — this is a scan/read tool, not a gallery)

### Grid & Container
- **Max width**: 480px for single-column mobile-first pages (hub, disclaimer flow — matches existing `.wrap { max-width:480px }`), 1080–1200px for wide data tables/guide pages on desktop
- **Table pages**: full-width scrollable container with `overflow-x:auto` on mobile rather than forcing column collapse, since row identity (ticker + all indicators) must stay intact

### Whitespace Philosophy
Unlike Tesla's "one message per screen" gallery pacing, this system uses
whitespace *inside* and *between* cards to create scannable rhythm across a
dense list — the goal is a reader moving quickly through 20–100 rows of
signals without eye strain, not a slow cinematic scroll. Padding inside
cards/rows does the work; the page overall stays compact.

### Border Radius Scale
| Value | Context |
|-------|---------|
| 8px | Buttons, inputs |
| 12px | Cards, disclaimer boxes |
| 16px | Larger feature cards / modals |
| 999px | Badges, pills |

## 6. Depth & Elevation

| Level | Treatment | Use |
|-------|-----------|-----|
| Level 0 (Flat) | No shadow, hairline border only | Table rows, inline text, nav |
| Level 1 (Card) | `0 1px 2px rgba(10,11,13,0.04)` + `1px solid #E3E6EA` | Default card/module state |
| Level 2 (Hover) | `0 2px 8px rgba(10,11,13,0.08)` | Clickable card/table row hover |
| Level 3 (Overlay) | `0 8px 24px rgba(10,11,13,0.12)` | Modals, dropdown menus, tooltips |

### Shadow Philosophy
Unlike Tesla's zero-shadow doctrine, this system uses *very* soft shadows
deliberately: a data card needs to read as a distinct, trustworthy "unit" of
information the way a bank statement line item does. Shadows stay low-alpha
(4–12%) and tight-radius — never a glow or dramatic drop shadow. Combined
with the 1px hairline border, elevation communicates "this is a discrete,
verified data module," not decoration.

## 7. Do's and Don'ts

### Do
- Keep the page background off-white/light-gray (`#F7F8FA`) so white cards visibly separate
- Reserve green/red exclusively for actual price/signal direction — never for arbitrary success/error UI states unrelated to market data
- Use tabular-nums on every numeric column so tables scan cleanly
- Keep a 1px hairline border on every card and table row group
- Use soft, low-alpha shadows only — nothing above ~12% opacity
- Keep the disclaimer/callout box visually distinct but calm (neutral gray, not alarming red) unless content is genuinely a warning
- Use pill-shaped badges with tint backgrounds for signal states (SETUP/BREAKOUT/NONE)
- Keep transitions short (0.15–0.2s) and color/shadow-only — no scale or translate

### Don't
- Don't introduce photography or hero imagery — this is a data tool, not a brand showroom
- Don't use blue for anything except CTAs, links, and active/focus states — it must stay meaningful, not decorative
- Don't color a table row or number green/red unless it reflects an actual gain/loss or signal state
- Don't remove the card border in the name of "cleaner" design — the hairline is what makes dense tables/cards parseable
- Don't use uppercase for body copy or descriptions — reserve it for table headers and small badges only
- Don't add drop shadows heavier than the Level 3 spec — this system stays quiet, not "elevated SaaS with glowing cards"
- Don't override the system font stack with a webfont — these are static, no-build-step pages and load speed/CJK correctness matter more than brand typography

## 8. Responsive Behavior

### Breakpoints
| Name | Width | Key Changes |
|------|-------|-------------|
| Mobile | <480px | Single column, `.wrap` max-width 480px pattern, cards full-width, tables horizontally scrollable |
| Tablet | 480–1024px | Cards may go 2-up in grid contexts (not hub page), tables gain more visible columns |
| Desktop | >1024px | Guide/table pages use full 1080–1200px container; hub-style pages stay capped at 480–560px (they're meant to be read like a mobile card list even on desktop) |

### Touch Targets
- Card tap targets: full card is clickable, minimum 44px effective height
- Table rows (if row-level links exist): minimum 40px row height
- Buttons/inputs: minimum 40px height

### Collapsing Strategy
- **Tables**: horizontal scroll with a sticky first column (ticker) rather than hiding columns — every indicator must stay visible/reachable, not hidden behind a "more" toggle, since the columns are the entire point of the AND/W-pattern scan
- **Cards**: never go multi-column below tablet width; stacked single column is the default and often the final state (matches current hub page)

## 9. Agent Prompt Guide

### Quick Color Reference
- Primary CTA / links: "Coinbase Blue (#0052FF)"
- Page background: "Page Ground (#F7F8FA)"
- Card background: "Pure White (#FFFFFF)" with "Border Hairline (#E3E6EA)"
- Heading / price text: "Ink (#0A0B0D)"
- Body text: "Slate (#5B616E)"
- Metadata: "Steel (#8A919E)"
- Positive/gain: "Gain Green (#05B169)" on "Gain Green Tint (#E6F9EF)"
- Negative/loss: "Loss Red (#DF1B41)" on "Loss Red Tint (#FCE9EC)"
- Pending/setup: "Caution Amber (#F4A81E)" on tint `#FEF6E7`

### Example Component Prompts
- "Create a hub card: white background, 1px #E3E6EA border, 12px border-radius, 18px padding, a bold 16px Ink title with an emoji, a 12.5px Slate description below, an 11.5px Steel metadata line, and a trailing Steel chevron — subtle shadow on hover only, no transform"
- "Build a scan-result table row: white background, bottom border 1px #F0F1F3, ticker left-aligned in Ink 14px 600, numeric columns right-aligned with tabular-nums, percentage change colored #05B169 if positive / #DF1B41 if negative"
- "Design a signal badge pill: 999px border-radius, 4px 10px padding, 12px fontWeight 600 text, bg #E6F9EF text #05B169 for BREAKOUT, bg #FEF6E7 text #F4A81E for SETUP"
- "Create a primary button: bg #0052FF, white text, 14px fontWeight 600, 8px border-radius, 10px 20px padding, 40px min-height, hover darkens to #0040CC, transition background-color only 0.15s"
- "Design a disclaimer callout: bg #F7F8FA, 12px border-radius, 12px 14px padding, warning emoji + 12.5px fontWeight 500 Ink text in a flex row with 8px gap"

### Iteration Guide
1. Every numeric table/column change must preserve tabular-nums alignment — verify visually, misaligned digits break the "trustworthy data tool" impression instantly
2. Green/red must always trace back to an actual signal or price direction in the data — if you're reaching for green/red decoratively, use blue or gray instead
3. When adding a new page type, start from the card or table pattern already in this file rather than inventing new elevation/radius values
4. Keep language-neutral spacing: Korean/Japanese line-height needs the same 1.5–1.6 generosity as Korean text is denser per character than English
5. If a screen starts to feel like a "marketing landing page," pull back — this system is Coinbase's product/dashboard register, not their marketing site

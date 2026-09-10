# Design System Inspired by Tesla

## 1. Visual Theme & Atmosphere

Tesla's website is an exercise in radical subtraction — a digital showroom where the product is everything and the interface is almost nothing. There are no decorative borders, no gradients, no patterns, no shadows. The UI exists only to provide just enough navigational structure to get out of the way. Every pixel that isn't product imagery is white space, and that restraint is the design system's most powerful statement.

The color philosophy is almost ascetic: a single blue (`#3E6AE1`) for primary calls to action, three shades of dark gray for text hierarchy, and white for everything else. This project has no product photography, so whitespace and typographic restraint — not imagery — carry the "gallery silence" that Tesla achieves with cinematic photography. Discipline in what is *not* shown is the design statement.

Typography uses a single Universal Sans family — a custom family split into "Display" for headlines and "Text" for body/UI elements. There are no text shadows, no text gradients, no decorative type treatments. Every letterform earns its place through clarity alone.

**Key Characteristics:**
- Near-zero UI decoration: no shadows, no gradients, no borders, no patterns anywhere on the page
- Single accent color — Electric Blue (`#3E6AE1`) — used exclusively for primary CTA buttons and interactive elements
- Universal Sans font family (Display + Text) as the only typeface, everywhere
- Whitespace-first presentation — restraint carries the emotional/trust weight that photography would on a product site
- 0.33s cubic-bezier transitions as the universal timing for all interactive state changes (color/background only — no transform, no scale)
- lowercase, normal-tracking typography throughout — no uppercase transforms, no letter-spacing tricks
- One narrow, explicitly-scoped exception exists for this project's core function: signal/gain-loss color (§2.6) — everything else in the system stays strictly monochrome + Electric Blue

## 2. Color Palette & Roles

### Primary
- **Electric Blue** (`#3E6AE1`): Primary CTA button background, links, active/interactive states — a confident, mid-saturation blue (rgb 62, 106, 225) that stands alone as the primary chromatic color in the interface. Used for "primary action" buttons and any element the user should act on
- **Pure White** (`#FFFFFF`): Dominant background color for all surfaces, panels, navigation

### Surface & Background
- **White Canvas** (`#FFFFFF`): Page background and all surface containers
- **Light Ash** (`#F4F4F4`): Subtle alternate surface for section differentiation and table zebra rows — barely perceptible shift from pure white (rgb 244, 244, 244). This is the *only* mechanism allowed for separating rows/sections when borders are forbidden (§4, Data Table)
- **Carbon Dark** (`#171A20`): Dark surface color for any dark-mode/overlay contexts (rgb 23, 26, 32)

### Neutrals & Text
- **Carbon Dark** (`#171A20`): Primary heading and navigation text (rgb 23, 26, 32)
- **Graphite** (`#393C41`): Body text and secondary content (rgb 57, 60, 65)
- **Pewter** (`#5C5E62`): Tertiary text for sub-links, secondary labels (rgb 92, 94, 98)
- **Silver Fog** (`#8E8E8E`): Placeholder text, metadata, disabled states (rgb 142, 142, 142)
- **Cloud Gray** (`#EEEEEE`): Light dividers where absolutely unavoidable (prefer spacing instead — see §7)
- **Pale Silver** (`#D0D1D2`): Subtle UI delineation, same caveat as above

### §2.6 Semantic Signal Color — Scoped Exception
This project scans stocks for buy signals and must show price direction and
signal state at a glance; a strictly monochrome-plus-blue palette cannot
carry that meaning. This is the **only** sanctioned deviation from "Electric
Blue is the only chromatic color," and it is deliberately narrow:

- **Gain Green** (`#1DB954`): positive price change (%), "signal triggered / met" state
- **Loss Red** (`#D93025`): negative price change (%), "not triggered / bearish" state
- Two allowed forms only:
  1. **Text color** on numbers/labels that represent an actual price/signal direction (e.g. `+2.4%`, `BREAKOUT`)
  2. **Fill of a small solid indicator dot** (a single filled circle, ≤10px) that restates whether one specific signal/indicator has fired — this is a compact visual echo of the same signal information, not decoration
- Never as a background fill, chip/badge tint, row-highlight tint, or border, and never for anything that isn't literally a gain/loss/signal value. A "NEW"/"met all conditions" marker is bold text in Gain Green with no background — not a filled chip
- No third semantic color (no amber/warning) — a pending/partial state uses Pewter/Silver Fog (neutral, not-yet-triggered) rather than a new hue; only fully-triggered and not-triggered get Gain Green/Loss Red
- Everywhere else on every page — nav, buttons, headings, cards, links, disclaimers — stays exactly monochrome + Electric Blue. This exception does not open the door to any other color

### §2.7 Compliance Banner — Out of Scope
`assets/investment-warning.css` (`.site-investment-warning`, shared across
every published page) is a legal/compliance disclaimer banner, deliberately
built to be loud and non-dismissible (saturated red background, bold white
text, 2px border). It is **explicitly out of scope for this design system**
— do not restyle it to Electric Blue/monochrome or fold it into the §2.6
signal-color exception. Leave its markup and CSS exactly as-is; every other
element on the page still follows this system.

### Gradient System
- No gradients are used anywhere in the interface, including within the signal-color exception
- Depth is achieved entirely through whitespace, never through gradient or shadow

## 3. Typography Rules

### Font Family
- **Display**: `Universal Sans Display`, -apple-system, "Apple SD Gothic Neo", "Malgun Gothic", "Hiragino Sans", Arial, sans-serif — hero/page titles only (40px)
- **Text/UI**: `Universal Sans Text`, -apple-system, "Apple SD Gothic Neo", "Malgun Gothic", "Hiragino Sans", Arial, sans-serif — everything else: navigation, body copy, buttons, table content, product names
- No OpenType features, no italics

### Hierarchy

| Role | Size | Weight | Line Height | Letter Spacing |
|------|------|--------|-------------|-----------------|
| Hero/Page Title | 40px | 500 | 1.20 | normal |
| Product/Ticker Name | 17px | 500 | 1.18 | normal |
| Nav Item | 14px | 500 | 1.20 | normal |
| Body Text | 14px | 400 | 1.43 | normal |
| Button Label | 14px | 500 | 1.20 | normal |
| Sub-link | 14px | 400 | 1.43 | normal |
| Table Header / Cell | 14px | 400 (500 for header) | 1.43 | normal |

### Principles
- **Only two weights**: 500 (headings/UI/emphasis) and 400 (body). No bold (700), no light (300)
- **Only two sizes matter**: 14px for essentially all UI, 40px reserved strictly for hero/page titles. Don't invent intermediate sizes
- **Normal letter-spacing everywhere** — no negative tracking on headlines, no uppercase tracking tricks
- **No uppercase text transforms anywhere** — lowercase/sentence case only, including table headers and badges
- **Display vs Text split**: Display only for the single largest title on a page; Text for literally everything else, including large numeric values like prices

## 4. Component Stylings

### Buttons
All buttons: 4px border-radius, sharp technical aesthetic.

**Primary CTA**:
- bg `#3E6AE1`, text `#FFFFFF`, fontSize 14px, fontWeight 500, borderRadius 4px, minHeight 40px, width 200px
- Border: 3px solid transparent (reserves space for focus animation)
- Transition: `border-color 0.33s, background-color 0.33s, color 0.33s`
- Hover: subtle darkening of blue background only — no scale, no translate

**Secondary CTA**:
- bg `#FFFFFF`, text `#393C41`, same dimensions/border pattern as primary

**Nav Button**:
- bg transparent, text `#171A20`, fontSize 14px, fontWeight 500, borderRadius 4px, padding 4px 16px, minHeight 32px

**Text Link**:
- text `#5C5E62`, no background, no border, underline on hover only

Maximum two CTA buttons visible on any single screen/section.

### Cards & Containers
- Background: white or transparent (inherits page white)
- Border: **none**
- Shadow: **none**
- Separation between cards/sections is spacing only (minimum 16px gap, prefer 24–32px)
- Border radius: 0px default; up to 12px only for large image-scale surfaces (not applicable here since there is no photography — keep interactive cards at 0–4px)

### Data Table (Scan Results — `sp500_table.html`, `wpattern_table.html`)
Tesla's own site has no data tables, so this pattern is derived from the
system's principles rather than copied directly:
- **No borders anywhere in the table** — no cell borders, no outer border, no rules
- Row separation achieved purely through: (a) generous row height (min 40px), (b) alternating background between `#FFFFFF` and `#F4F4F4` (Light Ash) — this is the one exception where a background shift substitutes for a border, since it's "spacing made visible" rather than a decorative line
- Header row: fontWeight 500, `#171A20`, no background fill, separated from body purely by an extra 8px of top/bottom padding (not a rule)
- Numeric cells: plain text, right-aligned, `#393C41` (Graphite) by default
- **Signal/change cells only**: colored per §2.6 (Gain Green `#1DB954` / Loss Red `#D93025`), as text color or a small solid indicator dot — never a chip/background, and never a full-row background tint
- A per-indicator status dot (fired/not-fired) may use Gain Green/Loss Red fill; a *partial/pending* state uses a neutral (Pewter/Cloud Gray) dot, not a third color
- Row hover (if interactive): background shifts to `#F4F4F4` only — no border, no shadow, and never a colored row tint even for fully-met rows

### Inputs & Forms
- Background: transparent, text `#171A20`, placeholder `#8E8E8E`
- Border: none at rest; on focus, a single 1px `#3E6AE1` bottom rule only (closest Tesla equivalent to a focus indicator without a boxed border)
- Font: Universal Sans Text, 14px

### Navigation
- White background, no border, no shadow — the nav blends with the page via whitespace alone
- Active nav item: text `#3E6AE1`

## 5. Layout Principles

### Spacing System
- **Base unit**: 8px
- **Common values**: 8px, 16px, 24px, 32px
- **Section spacing**: generous — treat each major section like a Tesla viewport-height section where the content allows (hub/guide pages); dense scan tables may compress this out of necessity but must still use spacing (never borders) between the table and surrounding content

### Grid & Container
- **3-column grid on desktop, 2-column on tablet, 1-column on mobile** for any card/link grid (hub pages, category-style listings)
- **Max width**: content-appropriate (480px for mobile-first hub pages, wider for data tables), full-bleed avoided in favor of centered content with generous side margins

### Whitespace Philosophy
Whitespace is the luxury signal. Never fill available space just because it's empty. On this project specifically: resist the urge to add dividers, boxes, or borders to "organize" a page — add space instead. A page that feels sparse is working correctly.

### Border Radius Scale
| Value | Context |
|-------|---------|
| 0px | Default — sharp edges everywhere |
| 4px | Buttons, nav items only |

## 6. Depth & Elevation

| Level | Treatment | Use |
|-------|-----------|-----|
| Level 0 (Flat) | No shadow, no border | Default and only state for every element on the page |

### Shadow Philosophy
No box-shadows anywhere, no exceptions. Depth is communicated only through spacing and z-index/positioning where strictly necessary (e.g. a dropdown appearing above content) — never through shadow, border, or gradient.

## 7. Do's and Don'ts

### Do
- Use Electric Blue (`#3E6AE1`) exclusively for primary CTAs and links — never decoratively
- Keep typography at weight 400–500 only, sizes clustered at 14px with 40px reserved for hero titles
- Use 4px border-radius for buttons/nav only; 0px everywhere else
- Trust whitespace — never fill space just because it's empty
- Keep all transitions at 0.33s, color/background only
- Use lowercase/sentence-case text everywhere, no uppercase transforms
- Separate table rows and sections with spacing (and, only in tables, the Light Ash zebra background) — never a border
- Apply Gain Green / Loss Red **only** to actual price-change or signal-state text (§2.6) — nothing else may use color

### Don't
- Add shadows to any element
- Use any color besides Electric Blue and the §2.6 signal-color exception — no new accent colors, ever
- Apply gradients or decorative backgrounds
- Use text larger than 40px, or introduce sizes outside the defined hierarchy
- Add borders to cards, containers, or table cells — separation is spacing only
- Use uppercase text transforms
- Introduce large border-radii or pill shapes — 4px is the maximum, and only on buttons/nav
- Add hover animations with scale/translate transforms — interactions are color-only
- Put more than two CTA buttons in one screen/section
- Turn the §2.6 exception into a general-purpose UI color (e.g. don't use green for "success" toasts unrelated to price/signal data)

## 8. Responsive Behavior

### Breakpoints
| Name | Width | Key Changes |
|------|-------|--------------|
| Mobile | <768px | Single-column, hero text scales to ~28px, CTA buttons stack vertically, grid becomes 1-column |
| Tablet | 768–1024px | 2-column grid, CTAs remain side-by-side |
| Desktop | >1024px | 3-column grid, hero at 40px, side-by-side CTAs |

### Touch Targets
- Primary CTA buttons: 200×40px minimum
- Nav buttons: minimum 32px height
- Table rows: minimum 40px height

### Collapsing Strategy
- **Grid**: 3-column → 2-column (tablet) → 1-column (mobile)
- **CTA pair**: side-by-side on desktop, stacked on mobile
- **Data tables**: horizontal scroll on mobile rather than hiding columns — every indicator must stay reachable

## 9. Agent Prompt Guide

### Quick Color Reference
- Primary CTA / links: "Electric Blue (#3E6AE1)"
- Background: "Pure White (#FFFFFF)"
- Heading text: "Carbon Dark (#171A20)"
- Body text: "Graphite (#393C41)"
- Tertiary text: "Pewter (#5C5E62)"
- Placeholder/metadata: "Silver Fog (#8E8E8E)"
- Alternate surface / table zebra row: "Light Ash (#F4F4F4)"
- Positive price/signal (text or indicator dot): "Gain Green (#1DB954)"
- Negative price/signal (text or indicator dot): "Loss Red (#D93025)"

### Example Component Prompts
- "Build a hero section: centered page title in Universal Sans Display 40px weight 500 Carbon Dark, a subtitle in Text 14px Pewter, and one Electric Blue primary CTA button, 4px radius, 200x40px — no shadow, no border, generous whitespace above and below"
- "Build a scan-result table row: white or Light Ash alternating background, no borders anywhere, 40px min row height, ticker in 14px weight 500 Carbon Dark, numeric columns right-aligned Graphite, percentage change colored Gain Green if positive / Loss Red if negative — text color only, no background chip"
- "Build a nav bar: white background, no border, no shadow, wordmark left, nav items 14px weight 500 Carbon Dark centered, Electric Blue for the active item only"
- "Build a 3-column card grid (2-column tablet, 1-column mobile): each card is borderless, shadowless, separated by 24px gaps, product name 17px weight 500 Carbon Dark, description 14px weight 400 Pewter"

### Iteration Guide
1. Focus on ONE component at a time — this system is minimal enough that every element must be pixel-perfect
2. Reference exact hex codes from this document — there are only 8 colors total in the entire system (6 monochrome + 2 signal)
3. If you're about to add a border or shadow, stop — replace it with spacing
4. If you're about to introduce a new color for anything other than an actual price/signal value, stop — use Electric Blue or a neutral instead
5. Verify lowercase/sentence-case text everywhere — no uppercase transforms slipped in from a component library default

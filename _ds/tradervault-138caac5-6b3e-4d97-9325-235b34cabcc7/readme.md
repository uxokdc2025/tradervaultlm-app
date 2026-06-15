# Intent UI Design System

**Intent UI** is a chill set of accessible React components built on top of [React Aria Components](https://react-spectrum.adobe.com/react-aria/) and Tailwind CSS. Easy to customize — just copy & paste into your React project. Includes [Intent Blocks](https://blocks.intentui.com) for rapid page design.

- **Website:** https://intentui.com
- **Docs:** https://intentui.com/docs/2.x/getting-started/introduction
- **GitHub:** https://github.com/intentui/intentui
- **Discord:** https://discord.gg/DYmVJ66JUD
- **Author:** [@irsyadadl](https://x.com/irsyadadl)
- **License:** MIT

> **Sources used to build this design system:** The GitHub repo [`intentui/intentui`](https://github.com/intentui/intentui) was the primary source. The `resources/styles/app.css`, `resources/colors/colors.json`, and all files under `components/ui/` were read and translated into this design system. Fonts (`InterVariable.woff2`, `GeistMono[wght].woff2`) were imported directly from the repo. Readers with access to the repo are encouraged to explore it further — the component implementations there (using `tailwind-variants` and React Aria) are the ground-truth reference.

---

## Content Fundamentals

Intent UI has a casual, developer-friendly voice. Think of it as a knowledgeable friend who happens to know a lot about React accessibility — not a corporate tech manual.

### Tone & Voice
- **Chill, friendly, direct.** The tagline is literally "Intent is a chill set of React components."
- **First person plural (we) sparingly; second person (you) preferred.** "Just copy & paste into your React projects."
- **Active voice only.** Never passive.
- **Casual contractions OK.** "You'll", "it's", "don't."
- **Slang is welcome but not forced.** "Peep the docs," "get the lowdown," "swing by" — these appear in the README. But never forced; it comes naturally.
- **No corporate jargon.** No "leverage," "synergy," "best-in-class."
- **Emoji:** Not used in UI components. Appear sparingly in docs prose for personality (1 per paragraph max). Never in component labels, buttons, or status text.

### Casing
- **UI labels:** Title Case for navigation items, sentence case for descriptions.
- **Error messages:** Sentence case. "This username is already taken."
- **Button labels:** Short imperative verbs. "Save," "Cancel," "Delete," "Invite," "View all."
- **Component names:** PascalCase always in code. Sentence case in prose: "The button component."

### Copy Examples (from source)
- "Intent is a chill set of React components, built on top of React Aria Components"
- "Easy to customize and just copy & paste into your React projects"
- "Swing by intentui.com to peep the docs and get the lowdown on getting started!"
- "Design pages faster than ever with Intent Blocks"
- "Make sure to check out the contributing guide, and join our awesome list of contributors"

---

## Visual Foundations

### Colors
- **Primary:** Blue — `oklch(0.546 0.245 262.881)` (Tailwind blue-600). Used for interactive elements, focus rings, active states.
- **Neutral base:** Zinc scale — near-neutral with a very subtle blue-gray cast. Light mode uses zinc-50/100/200 for surfaces; dark mode uses zinc-900/950.
- **Dark mode background:** `oklch(0.091 0.005 285.823)` — extremely dark zinc, near-black.
- **Status colors:** Emerald for success, Amber for warning, Red for danger, Sky for info. All use translucent tints for badges/chips.
- **No gradients** on UI surfaces. The brand is clean and flat.
- **Color palette** is Tailwind's full palette in oklch values — all colors available as raw tokens (`--blue-600`, `--zinc-400`, etc.).

### Typography
- **Primary font:** Inter Variable (self-hosted woff2). Features `cv02`, `cv03`, `cv04`, `cv11` enabled for cleaner rendering.
- **Mono font:** Geist Mono Variable (self-hosted woff2). Used for code blocks, keyboard shortcuts, token names.
- **No display/serif font.** Entirely sans-serif.
- **Anti-aliasing:** `-webkit-font-smoothing: antialiased` always on.
- **Scale:** Tailwind-compatible rem scale. Body is 14px (0.875rem). Display starts at 36px (2.25rem).
- **Weight range:** 400 (body) → 500 (labels/medium) → 600 (headings/semibold) → 700 (display).
- **Letter spacing:** Negative tracking (`-0.02em` to `-0.03em`) on headings for tightness.

### Spacing
- **Base unit:** 4px (0.25rem). Everything is multiples of 4px.
- **Card padding:** 24px (`--card-spacing: 1.5rem`) inside cards.
- **Input height:** 40px (`h-10`). Buttons: 32px (xs) → 44px (lg).
- **Component gaps:** 8px between inline items, 16px between form fields, 24px between sections.

### Backgrounds & Surfaces
- **Light mode:** White bg (`oklch(1 0 0)`). Muted surfaces at zinc-100. No textures, patterns, or background images.
- **Dark mode:** Near-black zinc (`oklch(0.091)`). Overlay surfaces slightly lighter at `oklch(0.17)`. Sidebar/navbar slightly distinct: `oklch(0.16-0.17)`.
- **No gradients on surfaces.** The button *does* have a subtle `inset-shadow` for a slight 3D appearance, but no gradient fills.

### Animations & Motion
- **Easing:** `cubic-bezier(0.4, 0, 0.2, 1)` default; `cubic-bezier(0.34, 1.56, 0.64, 1)` spring for entrances.
- **Duration:** Fast (100ms) for micro-interactions (hover states); Normal (200ms) for transitions; Slow (300ms) for modals/overlays.
- **Entrance patterns:** Fade + slight translate-Y for dropdowns; Fade + scale(0.96) zoom for dialogs.
- **No looping decorative animations** on UI elements. The only loop is `blink` for loading dots.
- **`tw-animate-css`** is used for the animation library.
- **Reduced motion:** All entrance animations should be gated on `@media (prefers-reduced-motion: no-preference)`.

### Hover & Press States
- **Hover:** Darken by `color-mix(in oklch, <color> 92%, black)` for filled buttons. Lighten background (muted surface) for ghost/outline buttons.
- **Active/Press:** No shrink. Slight overlay darkening.
- **Disabled:** `opacity: 0.5`. `pointer-events: none`. No cursor-not-allowed on the element itself (but set on parent).
- **Focus rings:** 4px ring at `ring-color / 20% opacity` around focused elements. `outline: 2px solid var(--ring); outline-offset: 2px`.

### Borders
- **Input borders:** `var(--input)` = zinc-300 light / slightly lighter dark. On focus: primary color ring.
- **Card borders:** `var(--border)` = zinc-200 light / zinc-700 dark. Subtle, low-contrast.
- **Border radius:** `--radius-lg: 0.5rem` (8px) is the base. Buttons, inputs, cards all use `lg`. Badges default to `full` (pill). Dialogs use `xl` (10px).
- **Inset ring on buttons:** `box-shadow: inset 0 2px oklch(1 0 0 / 15%)` for the subtle white highlight on filled buttons (light mode only; removed in dark mode).

### Shadows
- **Light mode:** `shadow-xs` (1px, 5% black) on cards and inputs. Very subtle.
- **Dark mode:** Shadows are invisible → border does the job instead.
- **Dialogs/Overlays:** `shadow-lg` for floating surfaces.
- **No outer glow, no colored shadows.** All shadows are `oklch(0 0 0 / alpha)`.

### Cards
- **Border:** 1px `--border`
- **Radius:** `--radius-lg` (8px)
- **Shadow:** `shadow-xs`
- **Background:** `--bg` (white / near-black)
- **Internal padding:** `--card-spacing` = 24px
- **No colored card accents.** No left-border color stripes.

### Imagery
- **No brand illustrations** in the base system.
- **Avatar photos:** Real photography, no icons/avatars.
- **Color vibe:** Cool-toned, crisp, no grain or vintage treatment.
- **No background images on surfaces.**
- **Icons:** Lucide-style stroke icons via `@intentui/icons` package (see ICONOGRAPHY).

### Dark Mode
- Triggered by `.dark` class on `<html>`. Stored in `localStorage.currentTheme`.
- All semantic tokens remap automatically in `.dark` scope.
- Navbar/sidebar get distinct dark surfaces (slightly lighter than bg).
- Scrollbar color adapts via `--border` token.

---

## Iconography

### Icon System
Intent UI uses the **`@intentui/icons`** package — a custom icon set based on **Lucide** icons (2px stroke, rounded linecaps, 24×24 viewBox). This is referenced in components via named imports like `IconCheck`, `IconMinus`, etc.

- **Package:** `@intentui/icons` (npm)
- **Style:** Outline/stroke icons. 2px stroke width. Rounded linecaps and linejoin. 24×24 viewBox.
- **Base style:** Lucide-compatible. If the `@intentui/icons` package is unavailable, Lucide React is the direct substitute.
- **CDN fallback:** https://unpkg.com/lucide@latest/dist/umd/lucide.js
- **Size in components:** Icons within buttons are 16×16 (`size-4`). Standalone icons vary.
- **Color:** Icons inherit `currentColor`. Icon opacity at rest is 60% inside buttons (`text-current/60`), rising to 90% on hover.

### No Emoji Icons
Emoji are not used as icons in the UI. Text labels and SVG icons are always preferred.

### No Unicode Symbols
Unicode glyphs (✓ × →) are not used as icons. All iconography is SVG-based.

### Copied Assets
- `assets/logo.svg` — the Intent UI logomark (zinc-800 background, white path, stacked-squares motif)
- `assets/favicon.svg` — PNG-embedded favicon
- `assets/icon.svg` — app icon
- `assets/images/avatar-cobain.jpg` — sample avatar
- `assets/images/avatar-irsyad.jpg` — sample avatar
- `assets/images/example-sidebar.jpg` — sidebar screenshot reference

---

## File Index

```
Intent UI Design System
│
├── styles.css              ← CSS entry point (@import only)
├── readme.md               ← This file
├── SKILL.md                ← Agent skill definition
│
├── tokens/
│   ├── fonts.css           ← @font-face for Inter + Geist Mono
│   ├── colors.css          ← All color tokens (semantic + raw palette)
│   ├── typography.css      ← Font stacks, size scale, weight, leading
│   ├── spacing.css         ← 4px-base spacing scale + semantic aliases
│   ├── radius.css          ← Border radius scale
│   ├── shadows.css         ← Elevation shadows + focus ring
│   ├── animation.css       ← Durations, easings, keyframes
│   └── base.css            ← CSS reset + scrollbar + selection styles
│
├── assets/
│   ├── logo.svg            ← Intent UI logomark (24×24)
│   ├── favicon.svg         ← Site favicon
│   ├── icon.svg            ← App icon
│   ├── fonts/
│   │   ├── InterVariable.woff2
│   │   ├── InterVariable-Italic.woff2
│   │   └── GeistMono[wght].woff2
│   └── images/
│       ├── avatar-cobain.jpg
│       ├── avatar-irsyad.jpg
│       └── example-sidebar.jpg
│
├── components/
│   ├── buttons/
│   │   ├── Button.jsx      ← Button component (6 intents, 5 sizes)
│   │   ├── Button.d.ts
│   │   ├── Button.prompt.md
│   │   └── buttons.card.html
│   ├── feedback/
│   │   ├── Badge.jsx       ← Badge component (6 intents, 2 shapes)
│   │   ├── Badge.d.ts
│   │   ├── Badge.prompt.md
│   │   └── feedback.card.html
│   ├── layout/
│   │   ├── Card.jsx        ← Card + subcomponents
│   │   ├── Card.d.ts
│   │   ├── Card.prompt.md
│   │   └── layout.card.html
│   ├── data/
│   │   ├── Avatar.jsx      ← Avatar (5 sizes, 2 shapes)
│   │   ├── Avatar.d.ts
│   │   ├── Avatar.prompt.md
│   │   ├── Table.jsx       ← Data table (sortable, selectable, custom render)
│   │   ├── Table.d.ts
│   │   ├── Table.prompt.md
│   │   └── data.card.html
│   ├── forms/
│   │   ├── Input.jsx       ← Input field with label, description, error
│   │   ├── Input.d.ts
│   │   ├── Checkbox.jsx    ← Checkbox with label, description
│   │   ├── Checkbox.d.ts
│   │   ├── Select.jsx      ← Dropdown with options, separator, disabled
│   │   ├── Select.d.ts
│   │   ├── Switch.jsx      ← Toggle switch, 3 sizes
│   │   ├── Switch.d.ts
│   │   └── forms.card.html
│   ├── navigation/
│   │   ├── Tabs.jsx        ← Underline + pill tabs, badges
│   │   ├── Tabs.d.ts
│   │   └── navigation.card.html
│   └── overlays/
│       ├── Dialog.jsx      ← Modal with backdrop, alert variant
│       ├── Dialog.d.ts
│       ├── Toast.jsx       ← Notifications + ToastProvider + useToast
│       ├── Toast.d.ts
│       └── overlays.card.html
│
├── guidelines/
│   ├── colors-primary.card.html
│   ├── colors-neutral.card.html
│   ├── colors-semantic.card.html
│   ├── colors-charts.card.html
│   ├── type-display.card.html
│   ├── type-body.card.html
│   ├── type-mono.card.html
│   ├── spacing.card.html
│   ├── radius.card.html
│   ├── shadows.card.html
│   └── brand-logo.card.html
│
└── ui_kits/
    └── docs/
        └── index.html      ← Intent UI docs site recreation
```

### Components (39 total)

| Name              | Dir                      | Notes                                           |
|-------------------|--------------------------|------------------------------------------------|
| `Button`          | `components/buttons/`    | 6 intents, 5 sizes, circle shape, pending state |
| `Alert`           | `components/feedback/`   | 5 intents, icon, title, inline banner           |
| `Badge`           | `components/feedback/`   | 6 intents, circle + square shapes               |
| `Kbd`             | `components/feedback/`   | Keyboard shortcut key, sm/md/lg                 |
| `Progress`        | `components/feedback/`   | 4 sizes/intents, indeterminate animation        |
| `Skeleton`        | `components/feedback/`   | Shimmer; Line/Title/Avatar/Card presets         |
| `Spinner`         | `components/feedback/`   | 5 sizes, primary/muted/current intents          |
| `Accordion`       | `components/layout/`     | Single/multi-open, bordered + separated         |
| `Card`            | `components/layout/`     | Header/Content/Footer/Action sub-components     |
| `Disclosure`      | `components/layout/`     | Single collapsible section with toggle          |
| `Heading`         | `components/layout/`     | h1–h6 with Intent UI typography                 |
| `Link`            | `components/layout/`     | Styled anchor, primary/secondary/unstyled       |
| `Separator`       | `components/layout/`     | Horizontal or vertical divider                  |
| `Sidebar`         | `components/layout/`     | Sections, icons, badges, footer slot            |
| `AvatarGroup`     | `components/data/`       | Stacked overlapping cluster + overflow count    |
| `Avatar`          | `components/data/`       | Image + initials, 5 sizes, circle + square      |
| `DescriptionList` | `components/data/`       | Key/value pairs, columns + stacked layouts      |
| `Table`           | `components/data/`       | Sortable, selectable, custom cell renderer      |
| `Checkbox`        | `components/forms/`      | Label, description, controlled/uncontrolled     |
| `Input`           | `components/forms/`      | Label, description, error, prefix/suffix        |
| `NumberField`     | `components/forms/`      | Stepper +/− buttons, min/max/step clamping      |
| `Radio`           | `components/forms/`      | Single-choice; use with RadioGroup              |
| `RadioGroup`      | `components/forms/`      | Vertical/horizontal radio group wrapper         |
| `Select`          | `components/forms/`      | Dropdown, separator, disabled options           |
| `Slider`          | `components/forms/`      | Range input, live value, optional tick marks    |
| `Switch`          | `components/forms/`      | 3 sizes, label, description, controlled         |
| `TagGroup`        | `components/forms/`      | Single/multi-select tag chips                   |
| `TagInput`        | `components/forms/`      | Free-form tag entry (Enter/comma to add)        |
| `Textarea`        | `components/forms/`      | Multi-line, char count, error state             |
| `Breadcrumbs`     | `components/navigation/` | Trail nav, custom separator, 3 sizes            |
| `Navbar`          | `components/navigation/` | Logo, links, actions slot, sticky/fixed         |
| `Pagination`      | `components/navigation/` | Smart ellipsis, siblings, edge jump buttons     |
| `Tabs`            | `components/navigation/` | Underline + pill variants, badges, disabled     |
| `Dialog`          | `components/overlays/`   | Modal, alert variant, 4 sizes, Esc/backdrop     |
| `Menu`            | `components/overlays/`   | Dropdown menu, icons, kbd hints, danger item    |
| `Popover`         | `components/overlays/`   | Anchored panel, title, outside-click close      |
| `Toast`           | `components/overlays/`   | 4 intents, ToastProvider + useToast hook        |
| `Tooltip`         | `components/overlays/`   | 4 placements, hover delay, focus support        |

### Further Reading
- Source repo: https://github.com/intentui/intentui — browse `components/ui/` for all 70+ component implementations using React Aria + tailwind-variants.
- Live docs: https://intentui.com/docs/2.x — full API reference, copy-paste code, accessibility notes.
- Blocks: https://blocks.intentui.com — pre-built page sections.

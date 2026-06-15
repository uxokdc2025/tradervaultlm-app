# TraderVault LM — Project Brief
> Paste this into any Claude conversation before asking it to design or build anything for this app.  
> This is the source of truth for navigation, page keys, design tokens, and locked constraints.

---

## What's been built

| File | Status | Notes |
|---|---|---|
| `tokens.css` | ✅ Final | All design tokens — never hardcode values |
| `AppShell.dc.html` | ✅ Final | Shell, sidebar, account switcher, kill switch |
| `Overview.dc.html` | ✅ In progress | Main dashboard page |

---

## Navigation structure (locked)

The sidebar nav is **flat** (no nested dropdowns). Section labels are visual grouping only — they are not clickable.

```
Overview                          key: 'overview'

── STRATEGIES & ANALYSIS ──
  Strategies                      key: 'strategies'    icon: teal   #3DD5A8
  Analysis                        key: 'analysis'      icon: teal   #3DD5A8

── TRADING ──
  Chart & signals                 key: 'chart'         icon: amber  #FBB23A
  Journal                         key: 'journal'       icon: amber  #FBB23A
  Audit log                       key: 'audit'         icon: amber  #FBB23A

── COPY TRADING ──
  Accounts                        key: 'accounts'      icon: coral  #F87171
  Configure                       key: 'configure'     icon: coral  #F87171
  Signal sync                     key: 'signal'        icon: coral  #F87171

  ── divider ──
  Settings                        key: 'settings'      icon: gray   #8B95A4
```

### Nav item states
- **Rest**: icon = section accent color, label = `#8B95A4` (grey, WCAG AA), bg = transparent
- **Hover**: bg = `rgba(202,255,51,0.08)` (subtle lime tint), label stays grey
- **Active**: bg = section active tint, label = section accent, 3px inset left bar = section accent

### Section active tints
| Section | Active bg |
|---|---|
| Overview | `rgba(202,255,51,0.12)` |
| Strategies | `rgba(61,213,168,0.12)` |
| Analysis | `rgba(167,139,250,0.10)` |
| Trading | `rgba(251,178,58,0.10)` |
| Copy Trading | `rgba(248,113,113,0.10)` |
| Settings | `rgba(255,255,255,0.06)` |

---

## Page map (all routes)

| Page | Key | Section | Status |
|---|---|---|---|
| Overview | `overview` | — | In progress |
| Strategies | `strategies` | STRATEGIES | Not started |
| Analysis | `analysis` | STRATEGIES & ANALYSIS | Not started |
| Chart & signals | `chart` | TRADING | Not started |
| Journal | `journal` | TRADING | Not started |
| Audit log | `audit` | TRADING | Not started |
| Accounts | `accounts` | COPY TRADING | Not started |
| Configure | `configure` | COPY TRADING | Not started |
| Signal sync | `signal` | COPY TRADING | Not started |
| Settings | `settings` | — | Not started |

---

## Design tokens (summary)

All tokens live in `tokens.css`. Reference via `var(--tv-*)`. **Never hardcode hex values.**

### Brand colors
```css
--tv-sidebar-green: #CAFF33    /* lime — primary brand accent, logo, clock dot */
--tv-teal:   #3DD5A8           /* Strategies & Analysis */
--tv-purple: #A78BFA           /* Analysis accent (labels/badges) */
--tv-amber:  #FBB23A           /* Trading */
--tv-coral:  #F87171           /* Copy Trading */
--tv-red:    #FF6B6B           /* Kill switch */
--tv-green:  #5AC57A           /* Primary CTA button fill */
```

### Content surface (light mode default, dark mode via [data-theme="dark"])
```css
--tv-bg:        #F5F6F8        /* page background */
--tv-surface:   #FFFFFF        /* card / panel surface */
--tv-surface-2: #F0F2F5
--tv-surface-3: #E8EBF0
--tv-border:    #E4E7EC
--tv-border-2:  #D0D5DD
--tv-text:      #0F1724        /* primary text */
--tv-text-2:    #3D4756        /* secondary text */
--tv-muted:     #6B7585        /* muted text */
```

### Sidebar (ALWAYS dark — never re-themed)
```css
--tv-sidebar-bg:     #0F1724
--tv-sidebar-border: rgba(255,255,255,0.07)
--tv-sidebar-text:   #E6EDF3
--tv-sidebar-muted:  #7D8590
--tv-sidebar-label:  #3D4756
--tv-sidebar-green:  #CAFF33
```

### Semantic
```css
--tv-green-bg: #F0FAF3   --tv-green-text: #1A7A3C   --tv-green-border: #A7E8BC
--tv-red-bg:   #FFF0F0   --tv-red-text:   #B91C1C   --tv-red-border:   #FECACA
--tv-amber-bg: #FFFBEB   --tv-amber-text: #92400E   --tv-amber-border: #FDE68A
```

### Radius
```css
--tv-radius-sm: 5px   --tv-radius-md: 7px   --tv-radius-lg: 10px   --tv-radius-xl: 14px
```

### Spacing (4px grid)
```css
--tv-space-1: 4px  --tv-space-2: 8px  --tv-space-3: 12px  --tv-space-4: 16px
--tv-space-5: 20px --tv-space-6: 24px --tv-space-8: 32px  --tv-space-10: 40px
```

### Typography
```css
--tv-font-sans: "Inter", system-ui, sans-serif
/* sizes: 10px / 11px / 12px / 13px / 15px / 18px */
/* weights: 400 / 500 / 600 / 700 */
```

---

## Shell constraints (locked — do not change)

1. **Sidebar is always `#0F1724`** — dark in both light and dark mode. Never re-theme it.
2. **No center modals** — all overlapping panels open as right-edge drawers. The one exception is the Kill Switch `AlertDialog` (destructive action confirm only).
3. **Drawer spec**: 33% width default → 90% when maximized. Header has close (X) + title/subtitle + maximize toggle. Footer has status (left) + Cancel / Save draft / primary CTA (right).
4. **Kill Switch**: KILL button → `AlertDialog` confirm → "Kill all trades" (destructive red) + Cancel. Never fires immediately.
5. **Account switcher**: bottom of sidebar, expands upward. Supports Alpaca Paper, Alpaca Live, Binance Futures + "Connect new account".
6. **Live UTC clock**: bottom of sidebar, ticks every second via DOM ref (not re-render).
7. **Theme toggle**: `data-theme="dark"` on root `<html>`, persisted to `localStorage` key `tv-theme`. Sidebar stays dark in both themes.
8. **Split button** ("New strategy" in topbar): shared-bg primary + caret dropdown. Dropdown anchored to right edge, opens below.

---

## Typography rules

- Nav labels: 14px / weight 400 rest, 500 active
- Section labels: 9px / weight 700 / uppercase / `--tv-sidebar-label`
- Nav grey (rest): `#8B95A4` — passes WCAG AA on `#0F1724`
- Card headings: 15px / 700
- Body: 13px / 400
- Captions / badges: 10–11px / 500–600

---

## Component patterns (use these, don't reinvent)

| Pattern | Implementation |
|---|---|
| Buttons | Primary = `--tv-green` fill / `#0F1724` text. Secondary = `--tv-surface-2` + border. Ghost = transparent + border. Danger = `--tv-red-bg` + `--tv-red-text` |
| Badges | Use `--tv-badge-*` token trios: `live`, `paper`, `draft`, `default`, `ai` |
| Cards | `--tv-surface` bg, `--tv-border` 1px border, `--tv-radius-lg` (10px), `--tv-space-6` (24px) padding |
| Inputs | 40px height, `--tv-radius-md` (7px), focus ring: `box-shadow: 0 0 0 4px rgba(90,197,122,0.18)` + `--tv-green` border |
| Tables | `--tv-surface` bg, `--tv-border` row dividers, `--tv-surface-2` header bg, 13px body text |
| Status dots | 6px circle: green=live, amber=warning/draft, red=error/stopped |

---

## What NOT to do

- ❌ Don't add new hex colors — derive from existing tokens or use `color-mix()`
- ❌ Don't use `Inter` — it's already loaded via `--tv-font-sans`
- ❌ Don't center modals (except Kill Switch confirm)
- ❌ Don't make the sidebar light/white in any theme
- ❌ Don't add expandable/collapsible nav trees — the nav is flat
- ❌ Don't rename page keys — routing depends on the exact strings above
- ❌ Don't use emoji in UI elements
- ❌ Don't add gradient backgrounds to surfaces

---

## Engineering lessons — DC / React (learned in build)

### React.createElement style must be an object, never a CSS string
```javascript
// ✅ CORRECT — React accepts style as a plain object
React.createElement('div', { style: { display: 'flex', alignItems: 'center', borderRadius: '8px' } }, ...)

// ❌ WRONG — React rejects CSS strings and throws a silent {} render error
React.createElement('div', { style: 'display:flex; align-items:center; border-radius:8px;' }, ...)
```

**Rule:** Any helper method that returns a React element (icon builders, card builders, list item builders, etc.) must use **style objects** with camelCase keys, not CSS strings.

**DC template holes are fine** — `style="{{ cssString }}"` works because the DC runtime converts the CSS string to a React style object before passing it to React. Only direct `React.createElement` calls bypass this conversion.

### Avoid multi-value CSS transitions in template-hole style strings
The DC runtime's CSS-string-to-object parser may mishandle comma-separated transition values:
```css
/* ❌ Risky in a DC CSS string hole — comma may confuse parser */
transition: border-color 0.15s, box-shadow 0.15s;

/* ✅ Safe — single value */
transition: all 0.15s;
```

### Nested sc-for is not supported
```html
<!-- ❌ Breaks silently — do not put sc-for inside sc-for -->
<sc-for list="{{ cards }}" as="card">
  <sc-for list="{{ card.stats }}" as="stat">...</sc-for>
</sc-for>

<!-- ✅ Correct — precompute the inner list as a React element in renderVals() -->
<sc-for list="{{ cards }}" as="card">
  {{ card.statsEl }}   <!-- React element built with createElement + object styles -->
</sc-for>
```

### dynamic style-hover holes are not supported
```html
<!-- ❌ style-hover only accepts literal strings, not {{ }} holes -->
<button style-hover="{{ card.hoverStyle }}">

<!-- ✅ Use a literal value, or use onMouseEnter/Leave handlers instead -->
<button style-hover="background:var(--tv-surface-2)">
```

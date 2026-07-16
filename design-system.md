# AiMY Design System

The shared foundation for the Aimy ecosystem — one token layer, one component library, one AI interaction language. Everything is product-agnostic: any Aimy product builds on it and feels native to the same family.

**Living reference:** `index.html` (interactive, light/dark toggle, every component rendered with states).

---

## Principles

| Principle | Meaning |
|---|---|
| **Token-first** | No hard-coded colors or spacing in product code. Every value is a CSS variable; themes and per-product accents are a single swap. |
| **Product-agnostic** | Components carry no product copy or logic. Each product re-themes `--accent` and supplies content. |
| **Theme-aware** | Every surface works in light and dark. Test both before shipping. |
| **AI-native** | AI states (thinking, streaming, citations, suggestions) are first-class components, not afterthoughts. AI never applies changes silently — always review (accept/reject). |
| **Accessible by default** | `:focus-visible` rings, `prefers-reduced-motion`, AA contrast in both themes. Status is always carried by color **and** text/icon, never color alone. |

---

## 1. Color

### Neutral ramp `--d50 … --d950` (navy-tinted)

`--d50` = strongest text, `--d950` = deepest surface. The ramp **inverts** in light mode, so text/surface roles hold automatically.

| Token | Dark | Light |
|---|---|---|
| `--d50` | `#eef2f6` | `#10151b` |
| `--d100` | `#d8e0e8` | `#1c2630` |
| `--d200` | `#c8d2dc` | `#2a3540` |
| `--d300` | `#b0bcca` | `#3a4653` |
| `--d400` | `#8b9aaa` | `#566472` |
| `--d500` | `#637280` | `#637280` |
| `--d600` | `#4a5b6e` | `#6e7d8d` |
| `--d700` | `#2e3d50` | `#b0bcca` |
| `--d750` | `#233040` | `#c8d2dc` |
| `--d800` | `#1c2630` | `#d8e0e8` |
| `--d850` | `#141b24` | `#e4eaf0` |
| `--d900` | `#0d1117` | `#eef2f6` |
| `--d950` | `#080b10` | `#f7fafc` |

Roles: `--d50` primary text · `--d400` secondary/muted · `--d500` tertiary/placeholder · `--d600` faint labels/separators.

### Brand & accent

| Token | Dark | Light | Use |
|---|---|---|---|
| `--brand` | `#3369ff` | same | Primary CTA, focus rings, links, selection |
| `--brand-dim` / `--brand-glow` | 15% / 25% | 12% / 20% | Tints, focus halos |
| `--accent` | `#8b4ff4` | same | **The one token products re-theme.** Nav active, chip selection, chat caret, coach marks |
| `--accent-rgb` / `-dim` / `-glow` | — | — | Derivatives of the accent |
| `--teal` | `#6fdfe2` | `#0d8f95` | Secondary accent; darkened in light for text contrast |
| `--ai` | `linear-gradient(104deg, #0066ff 0%, #61adf1 47%, #6fdfe2 100%)` | same | AI provenance — gradients, model dot, progress fills |
| `--ai-text` | `#61adf1` | `#1f5fd0` | AI-blue text (badges, selected options) |

Rule: **focus is always `--brand`**, never the product accent — focus stays consistent across every Aimy product.

### Semantic status

Text/icon hues darken one step in light mode (dark-mode mid-tones fail contrast on white). Tint backgrounds stay pale.

| Token | Dark | Light | Bg token |
|---|---|---|---|
| `--ok` | `#17b26a` | `#0e9257` | `--ok-bg` green @ 12–14% |
| `--warn` | `#f79009` | `#b26205` | `--warn-bg` amber @ 12–14% |
| `--err` | `#f04438` | `#d92d20` | `--err-bg` red @ 12–14% |
| `--info` | `#0ea5e9` | `#067dc2` | `--info-bg` cyan @ 12–14% |

### Surfaces & helpers

| Token | Dark | Light |
|---|---|---|
| `--body-bg` | `#0f1215` | `#f4f6f9` |
| `--card-bg` | `#141b24` | `#ffffff` |
| `--card-bg-raised` | `#1c2630` | `#f7f9fc` |
| `--card-border` | `rgba(255,255,255,.07)` | `rgba(16,24,40,.10)` |
| `--card-border-hover` | `rgba(255,255,255,.14)` | `rgba(16,24,40,.18)` |
| `--card-border-focus` | `rgba(51,105,255,.4)` | same |
| `--panel-bg` (glass panel) | `rgba(13,17,22,.95)` | `rgba(255,255,255,.96)` |
| `--glass-bg` / `--glass-border` | dark glass | white glass |
| `--text-strong` | `#ffffff` | `#10151b` |
| `--hairline` | white @ 7% | ink @ 9% |
| `--code-bg` | `#0b0f14` | **same — code blocks stay dark in both themes** |

---

## 2. Typography

**Pairing:** **Urbanist** = primary (body, UI, labels) · **Poppins** = display (H1/H2/H3) · **JetBrains Mono** = code/tokens. All loaded 300–800 with italics.

Tokens: `--font-sans` (Urbanist) · `--font-display` (Poppins) · `--font-mono` · `--fst-normal` / `--fst-italic`.

### Scale (`--fs-*`)
`2xs` 10 · `xs` 11 · `sm` 12 · `base` 13 · `md` 14 · `lg` 16 · `xl` 18 · `2xl` 22 · `3xl` 28 · `4xl` 34 · `5xl` 46 (px)

### Weights (`--fw-*`)
light 300 · regular 400 · medium 500 · semibold 600 · bold 700 · extrabold 800

### Line height (`--lh-*`) / tracking (`--ls-*`)
lh: none 1 · tight 1.2 · snug 1.4 · base 1.55 · relaxed 1.75
ls: tighter −0.03em · tight −0.02em · normal 0 · wide 0.04em · wider 0.08em

### Roles

| Role | Font | Size / Weight / Tracking |
|---|---|---|
| Hero H1 | Poppins | 46 / 800 / −0.03em |
| Section H2 | Poppins | 24 / 800 / −0.02em |
| Sub-heading H3 | Poppins | 14 / 700 |
| Page title | Urbanist | 15 / 700 / −0.01em |
| Body | Urbanist | 13 / 500 |
| Card title | Urbanist | 12 / 600 |
| Nav item | Urbanist | 13 / 600 |
| Label / eyebrow | Urbanist | 10 / 700 / +0.1em, uppercase |
| Badge / pill | Urbanist | 9–10 / 700, uppercase |
| Mono | JetBrains | 11–12 / 400–500 |

---

## 3. Spacing, radius, motion, shadow, layout

- **Spacing** — 4px base: `--sp-1…--sp-15` = 4, 8, 12, 16, 20, 24, 32, 40, 48, 60. Card padding 16 (compact) or 20–24 (comfortable).
- **Radius** — `--r-xs` 4 · `--r-sm` 6 · `--r-md` 8 · `--r-lg` 10 · `--r-xl` 12 · `--r-2xl` 16 · `--r-pill` 9999. Radius scales with component size.
- **Motion** — `--t-fast` 150ms · `--t-base` 200ms · `--t-slow` 300ms. `--ease-out: cubic-bezier(.22,1,.36,1)` for enter, `--ease-spring: cubic-bezier(.34,1.56,.64,1)` for feedback. Everything respects `prefers-reduced-motion`.
- **Shadows** — `--shadow-sm/md/lg/xl`; black-based in dark, cool ink-based in light.
- **Layout** — three-zone shell everywhere: fixed topnav (60px, `--topbar-height`) → fixed sidebar (240px, `--sidebar-width`) → scrollable main. Dashboard grids: Tier-1 `repeat(4, 1fr)`, Tier-2 `1.5fr 1fr`.

---

## 4. Theming

- Dark is default. Light mode = `<html data-theme="light">`; toggle persists to `localStorage` (`aimy-ds-theme`), applied pre-paint (no flash).
- Overrides are **token-level** in `:root[data-theme="light"]` plus a small set of scoped chrome/component rules. Never fork component markup per theme.
- Exceptions that stay dark in both themes: code blocks (`--code-bg`).
- Both themes are contrast-audited: no text below 3:1 against its composited background.

---

## 5. Component inventory

### Components (base)
| Component | Classes | Notes |
|---|---|---|
| Buttons | `.btn` + `.btn-brand/ghost/err/warn/ok/accent`, `.btn-sm/.btn-lg` | Contextual color; 13/700; radius `--r-md` |
| Tags & badges | `.tag` + `tag-ok/warn/err/info/teal/ai/accent/neutral`, `.signal-badge` | Uppercase 700; semantic color + border tint |
| Chips & filters | `.chip` (`default/active/brand/ok/warn/err`), `.afs` strip | Active = accent |
| Dropdown | `.v2-dropdown` pattern | Keyboard, `aria-haspopup="listbox"` |
| Cards | `.card`, `.bcard`, `.narrative-card`, `.finding` | One `.tier-primary` per view |
| Form inputs | `.input`, `.field`, masked API-key input | Focus = brand; mask secrets |
| Feeds, donut, score ring, progress bars, chart primitives, annotations | see doc | Chart header = title + controls + stats + legend |
| Identity | `.avatar`, `.user-pill` | Avatar gradient = human; `--ai` gradient = AI actor |
| Overlays | `.modal-backdrop`/`.modal`, `.tooltip-wrap`/`.tooltip` | Destructive modals need confirmation |
| Empty & loading | `.skeleton`, `.empty-state`, spinner | Every surface handles loading / empty / error |

### Core UI
Tabs `.ds-tabs/.ds-tab` · Segmented `.seg/.seg-btn` · Button group `.btn-group` + `.icon-btn` · Menu `.menu-anchor/.menu/.menu-item` · Switch `.ds-switch` · Checkbox/radio `.ds-choice` · Slider `.ds-range` · Progress `.ds-progress` (+ `.ok/.warn/.err`) · Steps `.steps/.step` (done/active/pending) · Accordion `.acc` (`<details>`) · Breadcrumbs `.crumbs` · Pagination `.pager` · Divider `.ds-divider` (+ `.labeled`) · Banners `.banner.info/ok/warn/err` · Data table `.dtable` · Toolbar `.toolbar` · Split button `.split-btn` · Tree `.tree` (`<details>`) · Command palette `.cmdk` · Settings row `.settings-list/.settings-row` · Links `.link` (`inline/muted`)

### Data Display
Stat card `.stat-card` (semantic `.stat-delta.up/.down`) · List group `.list-group/.list-row` · Description list `.desc-list` (`<dl>`) · Timeline `.timeline/.tl-item` (semantic dots) · Avatar group `.avatar-group/.av` · Rating `.rating/.star.on` · Status & badges `.status-pill/.status-dot` (`online/busy/away/offline`, `.pulse`), `.count-badge` · Kbd `.ds-kbd` · Sparkline `.sparkline` · Gauge (SVG arc) · Progress circle `.pcircle` · Notification `.notif-list/.notif(.unread)` · Comment thread `.comment/.comment-replies` · Profile card `.profile-card`

### Feedback & Overlays
Drawer `.drawer-stage(.open)/.drawer-panel` · Popover `.pop(.open)/.pop-bubble` · Confirmation (popconfirm, `.pop-actions`) · Inline note `.inline-note(.ok/.warn)` · Coach mark `.coach-anchor/.coach-dot/.coach-card` · Loading overlay `.loading-stage/.loading-overlay/.loading-panel` · Error state `.error-state` + `.offline-bar` · Error pages `.error-page/.error-code` (404/500) · Type-to-confirm (modal + gated destructive button)

### Forms & Inputs
Field & states `.ds-field/.field-input` (`.is-error/.is-success` + `.field-help`) · Select `.ds-select` (+ `.is-error`) · Search `.search-field` · Textarea `.ds-textarea` (+ `.is-error`) · Date picker `.cal` (today outlined, selected accent) · Radio cards `.radio-cards/.radio-card` (`:has()`) · Stepper `.stepper` · File upload `.uploader` · Tag input `.tag-input/.tag-token` (+ `.is-error`) · Password `.pw-wrap/.pw-eye/.pw-meter` (weak/mid/good) · OTP `.otp` (+ `.is-error`) · Time picker `.time-picker/.time-panel/.time-opt` · Input group `.input-group/.ig-addon` · Copy field `.copy-field` · Dual range `.drange` · Upload progress `.upload-list/.upload-item` (uploading/done/error) · Error summary `.form-summary` (`role="alert"`, links to fields)

### AI Components
| Component | Classes | Notes |
|---|---|---|
| Thinking indicator | `.ai-thinking` + `.stream-cursor` | Animated dots; blinking cursor while streaming |
| Reasoning disclosure | `.reasoning` | "Thought for Ns", `<details>` |
| Response actions | `.ai-actions` | Copy / regenerate / thumbs (selected = `--ok`) |
| Citations & sources | `.cite`, `.source-list/.source-item` | Inline `[n]` chips → sources footer |
| Agent steps | `.agent-steps/.agent-step(.done/.running/.pending)` | Live tool-call trace with timings |
| Suggestion review | `.ai-suggestion` (`del`/`ins` diff) | **Accept / Reject — AI never applies silently** |
| Context chips | `.ctx-chips/.ctx-chip` | Files/pages/selection visible to prompt, removable |
| Model picker | `.model-picker` | `--ai` gradient dot + capability tag |
| Voice input | `.voice-btn(.recording)/.voice-wave/.voice-timer` | Idle vs recording waveform |
| Inline AI menu | `.ai-menu` | Selection toolbar: Ask AiMY / Improve / Shorten / Translate |
| Usage & disclaimer | `.usage-pill`, `.ai-disclaimer` | Quota + "AiMY can make mistakes" |

### AiMY Canvas (shared chat shell)
Float input bar `.aimy-float-bar/-input/-send` (thinking state) · Filter tray `.filter-tray/.filter-chip` · Canvas overlay `.aimy-overlay(.open)` · Chat messages `.chat-msg.user/.aimy` + `.msg-bubble` · AiMY toast `.aimy-toast` · AiMY badge `.aimy-badge`. Follows the theme (dark glass in dark, light glass in light). User bubble = accent tint; AiMY bubble = card surface.

---

## 6. States

Every interactive component documents its states statically (for Figma capture) via helper classes that mirror the real pseudo-states:

- `.is-hover` / `.is-active` / `.is-focus` — mirrors `:hover` / `:active` / `:focus-visible`
- `.open` / `.visible` / `.selected` / `.is-open` — forced-open overlays
- Coverage: buttons (5 states), inputs (default/focus/error/success/disabled), selection controls, nav/tabs/chips, all overlays open (menu, popover, confirm, tooltip, drawer, modal), row components (tree/notification/palette/time), error variants (select, textarea, tag input, OTP), strength meter, upload statuses.

---

## 7. Accessibility

- WCAG 2.1 AA target; both themes audited to ≥3:1 for all text (≥4.5:1 for body).
- Focus: `:focus-visible` only, 2px `--brand` outline, 2px offset. Never remove without replacement; never use the accent for focus.
- Native elements first: `<details>` accordions/trees, native checkbox/radio/range/select where possible.
- `prefers-reduced-motion: reduce` disables shimmer, pulses, spinners, lifts.
- Error summaries use `role="alert"` and receive focus on submit; every error state pairs color with text.
- Mask sensitive fields (API keys, passwords) by default.

---

## 8. Files

| File | Purpose |
|---|---|
| `index.html` | The design system — tokens, components, states, themes, live demos |
| `design-system.md` | This reference |

# AiMY Design System

The shared foundation for the Aimy ecosystem — one token layer, one component library, one AI interaction language. Everything is product-agnostic: any Aimy product builds on it and feels native to the same family.

**Living reference:** `index.html` (interactive, light/dark toggle, every component rendered with states).

---

## Principles

| Principle | Meaning |
|---|---|
| **Token-first** | No hard-coded colors or spacing in product code. Every value is a CSS variable; themes and per-product accents are a single swap. |
| **Product-agnostic** | Components carry no product copy or logic. Each product re-themes `--qa-accent` (the current product's accent token) and supplies content. |
| **Theme-aware** | Every surface works in light and dark. Test both before shipping. |
| **AI-native** | AI states (thinking, streaming, citations, suggestions) are first-class components, not afterthoughts. AI never applies changes silently — always review (accept/reject). |
| **Accessible by default** | `:focus-visible` rings, `prefers-reduced-motion`, AA contrast. Status is always carried by color **and** text/icon, never color alone. |
| **Color signals status directly** | `--ok` / `--warn` / `--err` / `--info` are full-saturation hues — green, amber, red, blue — used deliberately so a verdict reads at a glance. See §1. |
| **A tag is a name, not a sentence** | A label pill carries the NAME of a state, so it is capitalised like one: sentence case, and both words capitalised when there are exactly two — "Meeting Set" is a thing, "meeting set" is something that happened. Past two words it is a phrase and stays sentence case. Full capitals were doing volume rather than meaning, and they cost legibility at 12px because every word becomes the same rectangle. The one role that keeps capitals is the section marker, of which there is one per group. See §2. |
| **A label has a fill; a control has an edge; a link has neither** | A hairline border is this system's signature for something you can press. Tags and status labels take a ground and no border; buttons and chips take a border and no ground; a link is coloured text with neither. Anything carrying both a fill and an edge is a control impersonating a label, or the reverse — and a **verb** wearing the link's clothes is the third mistake, which is how an actions row ends up reading as a row of URLs. See §2, *Hierarchy*. |
| **A rank is a set of differences** | A rank differs from its neighbour in at least **two of {size, weight, ink}**. One axis is not a level: 14 against 16 at the same weight in the same grey is two things a reader cannot separate, and it reads as noise rather than as order. Both products wrote this rule for themselves before it was written here. See §2, *Hierarchy*. |

---

## 1. Color

### Neutral ramp `--d50 … --d950` (navy-tinted)

`--d50` = strongest text, `--d950` = deepest surface. The ramp is **re-derived** for light, not
inverted: the roles hold (ink at the `--d50` end, surfaces at the `--d950` end) but the values are
picked against a white ground, because dark-on-light reads heavier than light-on-dark. Ink steps
sit ~1.22× apart in contrast, and every one clears AA on both `--card-bg` and `--body-bg`.

| Token | Dark | Light | Role |
|---|---|---|---|
| `--d50` | `#f5f7fb` | `#0f172a` | Strongest ink |
| `--d100` | `#dee5ed` | `#1e293b` | Primary ink |
| `--d200` | `#c3ceda` | `#2e3747` | Secondary ink |
| `--d300` | `#a8b5c5` | `#3a4352` | Subtext |
| `--d400` | `#95a4b5` | `#45505f` | Muted |
| `--d500` | `#8898ac` | `#515e72` | Caption |
| `--d600` | `#7c8ea4` | `#5f6b7d` | Placeholder |
| `--d700` | `#2e3d50` | `#cfd8e3` | Dividers, decorative glyphs |
| `--d750` | `#233040` | `#e6ebf3` | Surface |
| `--d800` | `#1c2630` | `#f2f5fa` | Surface |
| `--d850` | `#141b24` | `#ffffff` | Card |
| `--d900` | `#0d1117` | `#edf1f6` | Panel |
| `--d950` | `#080b10` | `#e4e9f0` | Deepest ground |

### Surface wash ramp `--w015 … --w50`

Every hairline, subtle fill and hover in the system resolves through one ramp, so there are no
loose `rgba(255,255,255,…)` literals left in the library. Dark washes **white onto a dark ground**;
light washes **navy `#0f172a` onto a light ground** — navy rather than black, because a neutral
black wash reads grey and dirty. Alphas are re-tuned, not mirrored: hairlines (`--w07` and up) hold
their alpha because dark-on-light needs the presence, while broad fills drop ~25% because
dark-on-light reads heavier.

Steps: `--w015 --w02 --w025 --w03 --w04 --w05 --w055 --w06 --w07 --w08 --w09 --w10 --w11 --w12
--w13 --w14 --w15 --w16 --w18 --w20 --w22 --w40 --w50` (the suffix is the dark-mode alpha).

Companions: `--well` / `--well-strong` (recessed full-bleed strips — light grey recesses in light,
never black scrims) and `--shc-1/2/3` (shadow ink by weight; component geometry stays local, only
the ink is themed).

### Text / ink roles

| Role | Token | Dark | Light | Use |
|---|---|---|---|---|
| `--text-strong` | alias `--ink-primary` | `#f5f7fb` | `#0f172a` | Strong emphasis, headings |
| `--text-primary` | alias `--ink-secondary` | `#dee5ed` | `#1e293b` | Anything you read: figures, names, body |
| `--text-secondary` | — | `#c3ceda` | `#2e3747` | Secondary copy |
| `--text-subtext` | alias `--ink-muted` | `#a8b5c5` | `#3a4352` | Evidence lines, supporting metadata |
| `--text-muted` | — | `#95a4b5` | `#45505f` | Muted context |
| `--text-caption` | alias `--ink-rule` | `#8898ac` | `#515e72` | Caption / metadata, non-text rules |
| `--text-placeholder` | alias `--ink-placeholder` | `#7c8ea4` | `#5f6b7d` | A hint that must not read as a value |
| `--text-link` | — | `#7ea7ff` | `#1d4ed8` | Interactive text |

### Brand & accent

| Token | Dark | Light | Use |
|---|---|---|---|
| `--brand` | `#3369ff` | `#1d4ed8` | Primary CTA, focus rings, links, brand buttons, AI canvas accent |
| `--brand-rgb` | `51,105,255` | `29,78,216` | Tint base — use `rgba(var(--brand-rgb), α)`, never the literal |
| `--brand-dim` / `--brand-glow` | `rgba(…,.15)` / `.25` | `rgba(…,.10)` / `.18` | Tints, focus halos |
| `--qa-accent` ⚠ | `#8b4ff4` | `#6725cc` | **Placeholder** — borrowed from the Talent product. Nav active state, chip active, topnav tab active; one swap propagates everywhere. Replace with the QA-specific magenta from the Figma logo before v2 ships |
| `--qa-accent-rgb` / `-dim` / `-glow` | `139,79,244` / `.15` / `.25` | `103,37,204` / `.10` / `.18` | Derivatives of the accent |
| `--cyan` (alias `--teal`) | `#45d3e6` | `#096673` | Secondary accent — AI identity signals, eyebrows, version badge, gradient endpoint |
| `--cyan-rgb` | `69,211,230` | `9,102,115` | Tint base |
| `--cyan-bg` (alias `--teal-dim`) / `--cyan-border` | `rgba(…,.12)` / `.30` | `rgba(…,.10)` / `.28` | Tints, borders |
| `--purple` | `#8b4ff4` | `#6725cc` | Same value as `--qa-accent` |
| `--ai` | `linear-gradient(104deg, #0066ff, #61adf1 47%, #45d3e6)` | `linear-gradient(104deg, #0047c7, #1f6fc4 47%, #0a7a8c)` | AI provenance — gradients, model dot, progress fills. Darkened in light so it survives `background-clip:text` |
| `--ai-ink` / `--ai-ink-soft` | `#61adf1` / `#a8ccff` | `#0a57ac` / `#37618f` | The **readable** members of the AI ramp. The gradient is decoration; these carry text |
| `--ai-rgb` | `0,102,255` | `0,82,212` | Tint base for AI-tinted fills and borders |

Rule: **focus is always `--brand`**, never the product accent — focus stays consistent across every Aimy product.

### Semantic status — full saturation, and a mark is not a sentence

Status colors are deliberately vibrant so a verdict reads at a glance: green for pass, amber for
review/borderline, red for fail/critical, blue for informational. Each has a `-bg` tint and a
`-border` line at the same hue; filled/solid variants (`.tag-solid`) use the hue as a background
with `--text-on-status` for the label text — which is `#0d1117` in dark and `#ffffff` in light.

Light cannot reuse the dark hues — they were chosen to glow against near-black and sit at
1.6–2.6:1 on white. What light ships is **the bold family**, matched to Knowledge and Sales.

### The bold family, and the two jobs a hue has

Light once carried a set re-derived against a contrast target: a bottle green, a brown where amber
had been. Correct by the numbers, and it took the colour out of the one theme with room for it.
**The bold family is back**, and the deep set it replaced was not deleted — it was re-pointed to
the one role it is safe for.

The split is the whole idea. A hue does two jobs, and only one of them is reading:

- **`--ok` / `--warn` / `--err` / `--info` / `--cyan` are marks** — a ground, a border, a dot, an
  icon, a tag's edge. These answer to **3:1**, and the bold family clears it on both grounds.
- **`--ok-text` / `--warn-text` / `--err-text` / `--info-text` / `--cyan-text` are sentences.**
  These answer to **4.5:1**, and the deep set clears it on both grounds. In dark they are aliases
  of the hue, because a light hue on a dark ground needs no correction; light is the theme that
  needs its own values, and defines them. A component names the role once and gets the right ink in
  either theme instead of forking.

| Token | Dark | Light mark | card / body | Light sentence ink | card / body | Means |
|---|---|---|---|---|---|---|
| `--ok` | `#4ed6a1` | `#0e9257` | 3.99 / 3.52 | `#066640` | 7.04 / 6.22 | Pass, resolved, decided well |
| `--warn` | `#f7c95c` | `#b26205` | 4.52 / 4.00 | `#6b4500` | 8.48 / 7.49 | Review, at risk, needs attention |
| `--err` | `#ff7282` | `#d92d20` | 4.83 / 4.27 | `#a81029` | 7.58 / 6.69 | Fail, critical, decided badly |
| `--info` | `#7ea7ff` | `#067dc2` | 4.45 / 3.93 | `#1a54bd` | 6.89 / 6.09 | Informational, provenance |
| `--cyan` | `#45d3e6` | `#0d8f95` | 3.90 / 3.45 | `#096673` | 6.65 / 5.87 | AI provenance, secondary accent |
| `--err-strong` | `#ff5268` | `#b42318` | 6.57 / 5.81 | — | — | A control, not a label — see below |

Card is `#ffffff`, body is `#eef1f6`. **These are measured against this system's own grounds.**
Both products' libraries carry a table whose body column was taken on Sales's `#f4f6f9`; Knowledge
inherited that comment verbatim although its body is `#eef1f6`, so its stated figures run about
0.16 high. The conclusion survives the correction — the lowest mark is `--cyan` at 3.45 — but the
numbers in Knowledge are not Knowledge's.

**The tint is lighter than the ink, deliberately.** `--ok-bg` is a lighter green than `--ok`, which
is how the old family worked: the ground stays a wash while the word on it stays legible. `--ok-rgb`
tracks the **ink**, not the tint, because what reads it is some other alpha of the same hue.

### What the table above does not measure, and a tag does

Both figures above are the hue against a **flat** ground. A tag's word is not on a flat ground — it
sits on a tint **of its own hue**, which composites toward the ink and closes the gap. Measured on
the rendered components rather than derived:

| Tag | Ink | On a card | On the body |
|---|---|---|---|
| `.tag-ok` | `#0e9257` | 3.47 | 3.10 |
| `.tag-warn` | `#b26205` | 4.02 | 3.59 |
| `.tag-err` | `#d92d20` | 4.02 | 3.58 |
| `.tag-info` | `#067dc2` | 3.86 | 3.46 |
| `.tag-ai` / `.tag-teal` | `#0d8f95` | 3.29 | **2.94** |

So a light-mode tag reads between 2.9 and 4.0:1, and **`.tag-ai` on the body ground is the one that
misses 3:1 outright.** Cyan is the narrowest of the five to begin with — 3.90 on the card where the
next-lowest is 3.99 — and it is the only tag whose tint is struck from the same hex as its ink, so
it has the least room of any of them.

This is not a consequence of restoring the bold family here; it is a property of the family plus
the `.tag` rule, and **Knowledge and Sales carry it identically** — same tokens, same
`color: var(--ok)` on the tag. It is recorded rather than fixed because fixing it in this repo
alone would put the reference implementation's tags at a different colour from both products, which
is the thing this pass exists to stop. The fix, when it is made, is made in three places at once,
and the cheapest one is already in the system: `.tag-*` takes `--ok-text` instead of `--ok`, which
lands every tag between 5.0 and 7.5:1 without touching a single token value.

Each also has a matching `-rgb` companion (`--ok-rgb` etc.). **Always tint through the companion**
— `rgba(var(--ok-rgb), .1)` — never `rgba(78,214,161,.1)`, or the tint stays pinned to the dark hue.

| Token | Value | Notes |
|---|---|---|
| `--ok-bg` / `--ok-border` / `--ok-glow` | `rgba(78,214,161,.12)` / `.30` / `.20` | |
| `--warn-bg` / `--warn-border` | `rgba(247,201,92,.13)` / `.32` | No `--warn-glow` defined |
| `--err-bg` / `--err-border` / `--err-glow` | `rgba(255,114,130,.12)` / `.30` / `.20` | |
| `--info-bg` / `--info-border` | `rgba(126,167,255,.12)` / `.28` | |
| `--text-on-status` | `#0d1117` dark / `#ffffff` light | Ink on **solid** status fills. It inverts because a solid chip is bright in dark and deep in light |
| `--heat-ink` | `#0d1117` dark / `#0f172a` light | Ink on **heat-scale** fills. Near-black in both, because a heat cell is a saturated tint in both themes — do not use `--text-on-status` there |

**`--err-strong` is a control, not a label.** It stops something already *in flight* — hanging up
on a call mid-progress is the case it exists for. It is never a badge ground, never a border, never
status text; where a red is used to say what something **is**, that's `--err`.

**Tags carry the hue directly.** `.tag-ok` / `.tag-warn` / `.tag-err` / `.tag-info` / `.tag-teal` /
`.tag-ai` each take their tint as background, the full hue as text color, and a border at ~22%
opacity of the same hue — which is what puts their light-mode ink in the 2.9–4.0:1 band measured
above, `.tag-ai` worst. `.tag-qa` uses `--qa-accent`. `.tag-neutral` is a translucent white ground
with `--text-subtext`. `.tag-solid` variants fill with the full hue and switch to
`--text-on-status`.

### Surfaces & helpers

Dark marks elevation by getting **lighter**. Light cannot: once the card is white there is nowhere
lighter to go, so `--card-bg-raised` stays white and the lift moves into `--shadow-*`.

| Token | Dark | Light |
|---|---|---|
| `--body-bg` | `#0f1215` | `#eef1f6` |
| `--card-bg` | `#141b24` | `#ffffff` |
| `--card-bg-raised` | `#1c2630` | `#ffffff` (lift comes from shadow) |
| `--card-border` | `rgba(255,255,255,.07)` | `rgba(15,23,42,.10)` |
| `--card-border-hover` | `rgba(255,255,255,.14)` | `rgba(15,23,42,.18)` |
| `--card-border-focus` | `rgba(51,105,255,.4)` | `rgba(29,78,216,.45)` |
| `--panel-bg` (glass panel) | `rgba(13,17,22,.95)` | `rgba(255,255,255,.96)` |
| `--glass-bg` / `--glass-border` | `rgba(20,27,36,.85)` / `rgba(255,255,255,.08)` | `rgba(255,255,255,.80)` / `rgba(15,23,42,.10)` |
| `--glass-strong` / `--glass-soft` | `rgba(20,27,36,.90)` / `.65` | `rgba(255,255,255,.94)` / `.72` |
| `--topbar-bg` | `rgba(15,18,21,.88)` | `rgba(255,255,255,.85)` |
| `--panel-veil` (sidebar) | `rgba(10,13,17,.72)` | `rgba(255,255,255,.92)` |
| `--surface-deep` / `--surface-float` | `#151d28` / `#1e2428` | `#ffffff` / `#ffffff` |
| `--surface-sunken` | `#1a2330` | `#f2f5fa` |
| `--code-bg` / `--code-border` | `#0d1117` / `rgba(255,255,255,.07)` | **unchanged** / `rgba(15,23,42,.16)` |
| `--shc-1` / `-2` / `-3` (shadow ink) | `rgba(0,0,0,.20)` / `.35` / `.55` | `rgba(15,23,42,.05)` / `.09` / `.14` |

### Gradients

| Token | Value | Rule |
|---|---|---|
| `--ai` | `linear-gradient(104deg, #0066ff 0%, #61adf1 47%, #45d3e6 100%)` | AI identity only — logo, canvas strip, AI-scored badge bg. Light darkens it to `#0047c7 → #1f6fc4 → #0a7a8c` so it stays legible under `background-clip:text` |
| `--grad-avatar` | `linear-gradient(135deg, #7c3aed, #3369ff)` | All user avatars/pills, never non-user elements. Light: `#6d28d9 → #1d4ed8` |
| `--grad-display` | `linear-gradient(135deg, #fff 30%, var(--d300) 100%)` | Display-heading sheen. Light **must** run dark→mid (`#0b1220 → #4a5a73`) or the text disappears into the page |
| Ellipse · primary | `radial-gradient(ellipse at 30% 50%, rgba(0,102,255,.18) 0%, rgba(97,173,241,.1) 28%, transparent 60%)` | Fixed background layer, one per page, bottom-left. Light drops to ~⅓ alpha — at dark-mode strength an ambient wash reads as a smudge |
| Ellipse · secondary | `radial-gradient(ellipse at 75% 70%, rgba(69,211,230,.1) 0%, rgba(139,79,244,.07) 38%, transparent 60%)` | Fixed background layer, one per page, top-right. Same alpha reduction |

---

## 2. Typography

**One face:** **Poppins** sets every word — body, UI, labels and headings alike · **JetBrains Mono** = code/tokens. Poppins is loaded 300–700 with a 400 italic.

There is no pairing left. `--font-sans` and `--font-display` both name Poppins; the display token stays so its callers keep working, not because a second face is behind it. Urbanist is gone from the font request in all three products.

Tokens: `--font-sans` (Poppins) · `--font-display` (Poppins, the same face) · `--font-mono` · `--fst-normal` / `--fst-italic`.

**What the one face costs.** Poppins has no tabular figures, so every `font-variant-numeric: tabular-nums` in the system is inert and each count, duration and money column sets on proportional digits — a figure changes width when its value changes. Measured at 100px with the property set, digit-width spread is 63.00 for Poppins against 0.00 for a face that supports it, so this is the font and not the test. `--font-mono` is the only place in the system where a figure holds its width. If aligned figures are wanted back without giving up this face, the fix is a third token for numerals only, applied to elements that are PURELY a number and never to a sentence with one in it.

### Scale (`--fs-*`) — three sizes, and each one names what it is for

`2xs` 12 · `xs` 14 · `sm` 16 · `base` 16 · `md` 16 · `lg` 18 · `xl` 20 · `2xl` 24 · `3xl` 30 · `4xl` 38 · `5xl` 46 (px)

**12 — minimal components.** Tags, status labels, work states, and the metadata that sits beside
something else: a timestamp, a count, a unit, an attribution. Things you *recognise* rather than
read, three or four words at most. At 14 a tag stops behaving like a mark and starts competing with
the name next to it.

**14 — the smallest sentence.** A supporting line, help text, a dense cell, a control's label.
Anything with a verb in it starts here.

**16 — the working minimum.** Body, row text, card text, anything primary. Most of the product
lives here.

**Nothing is smaller than 12, and 12 is never a paragraph.** The old scale put four steps below 14
and body at 13, which is how the reference implementation alone accumulated **540 sites of sub-14px
type**; 341 of them were marks and 199 were ordinary text set too small. The upper steps moved up
with the base to keep the intervals — a heading one step above 16 has to be 18, not the 16 it used
to be.

### Every step is even, and the interval is +2

A scale that reads 12 · 14 · 16 · 18 has a decision in it. One that also holds 13, 15 and 17 has
none: nothing distinguishes the odd values from the even ones except which file they happened to be
typed in, and a 12 sitting beside a 15 is two components that were never compared. **A size is even
or it is a mistake** — round up, never down, because the floor is the thing being protected.

The rule is what makes the scale enforceable. "Under 14 is too small" catches nine and eleven and
lets thirteen through; "even, and never below twelve" catches all three, and a sweep can apply it
without a human deciding case by case. The one thing it cannot decide is whether something is a
mark or a sentence, so anything under 12 lands on **14** rather than 12 — 12 belongs to the
components that ask for it by name, and a sweep must not hand it out.

Three products ran on four scales — the shell's `--fs-*`, Sales's own `--fs-*` and `--ty-*`, and
Sales's surface scale `--t-*` — which is how 13 and 15 survived a floor that had already been
agreed. All four are now even.

**The reference implementation was the last one still off it.** Both products hold the rule on
their live surfaces — Knowledge renders 12/14/16/20 and Sales 12/14/16/18/20/26, neither with a
single run below 12 or on an odd step — while this page still carried **101 off-scale
declarations**, which resolved to 2,213 runs because the worst offenders were its most-reused
classes. They were 12.5, 13, 13.5, 15 and 17; the two fractional values alone accounted for 2,106
runs through `.ds-nav-link`, `.ds-desc`, `.ds-table` and `.ds-callout`.

98 were swept up to the next even step. Nine of them were library classes the products had already
moved and this file had not — `.input` and `.empty-state-desc` at 12.5 against their 14,
`.btn-lg`, `.chip-dismiss`, `.modal-body`, `.msg-bubble`, `.narrative-body` and `.surface-name` at
13 against their 14, `.surface-icon` at 15 against their 16. Every one of those nine lands on the
product's value under "round up to the next even step", so the rule and the products agree without
anything having to be decided case by case. That is the rule doing the job it was written for.

**Three are deliberately left off it**, because they are identical in this file, Knowledge and
Sales: `.aimy-float-input` and `.overlay-input` at 13.5, and `.nav-item` at 13. The first two are
the canvas and overlay inputs both products carved out of their own sweeps, on the rule that the
assistant must not look different depending on which product you opened it from; moving them here
alone would divide the three. They need one change made in all three repos, not one made here.

### Case — a tag is a name, a control is a verb

**Label pills** — `.tag`, `.work-state`, `.s-meta-st`, `.signal-badge`, `.trust-state`,
`.conf-badge`, `.model-tag`, `.ver-tag`, `.entry-mode-tag`, `.tc-approval` — are **sentence
case**, with **both words capitalised when there are exactly two**. A two-word label is the name of
a state ("Meeting Set", "Handed Over", "Not Saved"); at three words or more it has become a phrase
and title-casing it turns it into a headline, so it stays sentence case ("Do not call", "Up to
date"). A count is a measurement rather than a name and is left alone ("6 assets").

Full capitals were doing two jobs and only one was real: *this is a label, not prose* — which the
ground, the weight and the size already say. The other was volume, and a label has no business
being the loudest thing on a card. Capitals also cost legibility at 12px, because every word
becomes the same rectangle and the reader has to spell it.

**The tracking goes with the case.** `--ls-wide` is a correction *for* capitals; on sentence case it
is not a correction, it is gaps. A pill that drops `text-transform` drops `letter-spacing` in the
same edit.

**Where the rule is applied matters.** The same string is often a tag on one screen and a button or
a filter on another — `called['handed-over'].label` is all three in Sales. Title case belongs at the
render site, in a `tagCase()` helper, never on the table the string came from: in a tag it is a
name, and everywhere else it is doing a verb's work and takes sentence case.

**The one role that keeps capitals** is the section marker — `.b-cmeta-cap`, `.st-cap`,
`.menu-label`, a table head. There is one of them per group, it labels a region rather than an
object, and it is the single job `--ls-wide` exists for.

### Weights (`--fw-*`) — the ladder, re-cut for Poppins
light 200 · regular 300 · medium 400 · semibold 500 · bold 600 · extrabold 700

These numbers moved because the face changed. **The roles did not** — `--fw-bold` still means *the emphatic one*, it is just that in Poppins the emphatic one is 600.

Poppins lays down more ink than Urbanist at every weight, and the gap widens as it gets heavier. Measured in canvas as alpha per px of line length — typographic colour, which is what the eye actually reads:

| | Urbanist | Poppins, same number | drift |
|---|---|---|---|
| regular | 10.06 | 11.64 | +15.7% |
| medium | 11.65 | 14.12 | +21.2% |
| semibold | 13.74 | 16.60 | +20.8% |
| bold | 15.44 | 19.34 | +25.3% |
| extrabold | 16.83 | 21.37 | +27.0% |

Every rank landed a fifth to a quarter heavier than the value the surface was calibrated against — on the Knowledge console, 62 of 326 runs sat at 700 or above and 102 at 600 or above, a third of the page shouting. Poppins covers in 300–700 the colour range Urbanist covered in 400–800, so the whole ladder drops one step and lands back on the intended colour: regular −8.0%, medium −0.1%, semibold +2.8%, bold +7.5%, extrabold +14.9%.

**A raw number is outside the ladder, and the sweep is the whole job.** Changing the six tokens moves only what reads them. Every `font-weight: 700` written as a literal goes on rendering at a weight chosen for Urbanist, which is how all three products found the same fault after the face changed. The mapping is mechanical and identical everywhere:

```
800 -> --fw-extrabold (700)      600 -> --fw-semibold (500)
700 -> --fw-bold      (600)      500 -> --fw-medium   (400)
```

400 and below are left alone: the type floor is 400 or heavier under 18px, so `--fw-regular` at 300 is display-only and anything at 16px or under names `--fw-medium`, which still holds 400.

**The ladder is identical in Knowledge, Sales and the reference implementation on purpose.** All three ship this library and all three set Poppins; a ladder that differs between them is three design systems wearing one name.

### Line height (`--lh-*`) / tracking (`--ls-*`)
lh: none 1 · tight 1.2 · snug 1.4 · base 1.55 · relaxed 1.75
ls: tighter −0.03em · tight −0.02em · normal 0 · wide 0.06em · wider 0.08em

`--ls-wide` is the tracking for **capitals**, and capitals need 5–12%. It shipped at 4% — uppercase
with the correction left out — while the roles table below asked for +0.1em on the same runs, so
the token and the documentation disagreed and every component reading the token lost. Raised to
0.06em; `--ls-wider` is unchanged above it.

**The caption floor.** `--fs-2xs` is the smallest step in the system and no product may lower it.
It was 10px in the shell and 11px in Sales, on the argument that type that small is capitals and
tracked or it is not that size — which was the caps rule being used to justify the size rather than
the other way round. Both are 12 now, in every product, and the components that read the token got
the correction for free.

### Roles

| Role | Font | Size / Weight / Tracking |
|---|---|---|
| Hero H1 | Poppins | 46 / 700 / −0.03em |
| Section H2 | Poppins | 24 / 700 / −0.02em |
| Sub-heading H3 | Poppins | 18 / 600 |
| Page title | Poppins | 20 / 600 / −0.01em |
| Body | Poppins | 16 / 400 |
| Card title | Poppins | 16 / 600 |
| Nav item | Poppins | 16 / 500 |
| Label / eyebrow | Poppins | 14 / 600 / +0.06em, uppercase — the one role that keeps capitals |
| Tag / status / work state | Poppins | **12** / 600 / sentence case, both words capitalised at two words, 16px line box |
| Meta beside something | Poppins | 12 / 400–500 — a timestamp, a count, a unit, an attribution |
| Mono | JetBrains | 16 / 400–500 — inline `<code>` needs `font-size: 1em`, or the browser sets it to 13 |

### Hierarchy — a rank is a set of differences

The table above names the roles. This is how to combine them, and it is the
half that a type floor puts under pressure.

**A rank differs from its neighbour in at least two of {size, weight, ink}.**
One axis is not a level. 14 against 16 at the same weight in the same grey is
two things a reader cannot separate — the difference is there, and it reads as
noise rather than as order. Two axes moving together is what makes a hierarchy
read at a glance instead of on inspection.

**The floor compressed the size axis, so the other two have to absorb it.**
Before it, a product could spend five steps inside six pixels — 16 · 13 · 13 ·
12 · 12 · 12 · 10 was a real card in Sales. On even steps with a 12 floor there
are four: 12 · 14 · 16 · 18. Weight has five values and was carrying almost
nothing; ink has three that may hold type. Anything that used to be a size
difference is now a weight or an ink difference, and the ranks have to be
re-spread deliberately — **a floor applied without a hierarchy pass flattens
every card it touches.** Sales's queue card came out of the sweep with eleven of
seventeen runs at 16px, its name and its status sentence both 16/800/primary: a
card with two L1s that looked identical.

**Flatness is measurable, so measure it.** Take every text run in a block,
reduce it to the triple {size, weight, ink}, and count how many runs share the
commonest one. Above about **0.4 — nearly half the block wearing one face —
there is no hierarchy**, however carefully each treatment was chosen. Run it
across every surface in every role rather than judging by eye: it found four
blocks in Sales that reading the stylesheets had not.

The measure is a proxy and it misfires in one direction, so read the result
before acting on it. **A band is meant to be uniform** — a row of facts,
company · industry · city · headcount, is one rank and should wear one face,
and it scores high without being wrong. What the number is good at is finding
two *different* ranks that have collapsed onto one treatment.

**Three traps it found, none of them visible in the source:**

- **A demotion to a value the element already has is a no-op.** Sales's
  `.b-feed-meta` pushes an attribution to `--ink-muted` — and `--ink-muted` is
  `--d200`, which is what the line it sits in already sets. Written to move the
  bookkeeping a step down; after the ink band narrowed, moving it to exactly
  where it was. Seventeen of forty-two runs on a page came out identical
  because of it. **After narrowing a ramp, re-check every rule that demotes
  into it.**
- **One element, one rule.** Two rules set the same card title at two different
  tokens, same specificity, and the later one won — so the name rendered 16
  under a comment documenting it at 18. A second rule for an element is not an
  override, it is a coin toss decided by file order.
- **Emphasis inside a line needs the line not to be bold already.** A 700 line
  whose `<b>` runs inherit `bolder` gives you 700 and 800 in one sentence: two
  weights doing the work of none, and over two lines the mass of it outranks a
  larger heading above. Set the line a step down and let the emphasis be the
  step.

**A fact that is a door is still a fact.** A phone number, an email, a website,
a company name — values you read that happen to navigate. They take their row's
size, and colour carries that they are pressable; giving them their own size
makes a facts row alternate 16 · 14 · 16 · 16 on whether each fact happens to
be a link. A **verb** is not one of these. It is a control and takes the
control's edge — give it the link treatment and an actions row reads as a list
of URLs, which is what happened on a record where no primary was rendered at
all.

---

## 3. Spacing, radius, motion, shadow, layout

- **Spacing** — 4px base: `--sp-1…--sp-15` = 4, 8, 12, 16, 20, 24, 32, 40, 48, 60. Card padding 16 (compact) or 20–24 (comfortable).
- **Radius** — `--r-xs` 4 · `--r-sm` 6 · `--r-md` 8 · `--r-lg` 10 · `--r-xl` 12 · `--r-2xl` 16 · `--r-pill` 9999. Radius scales with component size.
- **Motion** — `--t-fast` 150ms · `--t-base` 200ms · `--t-slow` 300ms. `--ease-out: cubic-bezier(.22,1,.36,1)` for enter, `--ease-spring: cubic-bezier(.34,1.56,.64,1)` for feedback. Everything respects `prefers-reduced-motion`.
- **Shadows** — `--shadow-sm/md/lg/xl`; black-based in dark, cool ink-based in light.
- **Layout** — three-zone shell everywhere: fixed topnav (60px, `--topbar-height`) → fixed sidebar (240px, `--sidebar-width`) → scrollable main. Dashboard grids: Tier-1 `repeat(4, 1fr)`, Tier-2 `1.5fr 1fr`.

---

## 4. Theming

- Dark is default. Light mode = `<html data-theme="light">`; the toggle persists to `localStorage`
  (`aimy-ds-theme`) and is resolved pre-paint from an inline `<head>` script, so there is no flash.
  With nothing stored the page follows the OS `prefers-color-scheme` and keeps following it live.
  Switch it in the top bar or with <kbd>Shift</kbd>+<kbd>D</kbd>.
- Overrides are **token-level** in `:root[data-theme="light"]` (126 tokens) plus a handful of
  scoped rules for the toggle itself. No component forks its markup or its rules per theme.
- **Light is not dark inverted.** The two themes signal depth by opposite means — dark by getting
  lighter, light by casting shadow — and the dark accents sit at 1.6–2.6:1 on white, so they are
  re-derived rather than reused. See §1 for the per-token values.
- Exceptions that deliberately do **not** flip:
  | What | Behaviour | Reason |
  |---|---|---|
  | Code blocks | `--code-bg` and the `--syn-*` palette are inherited from `:root`; only `--code-border` changes | A snippet should read identically wherever it is quoted |
  | Colour specimens | Swatches in Color Tokens / Preserved foundation stay pinned to literal hex | They document the palette itself, so they must not move with the theme |
  | `--heat-ink` | Near-black in both themes | Heat-scale fills are saturated tints in both, so the ink must not follow `--text-on-status` |
- **Never hardcode.** Surfaces go through `--card-bg` / `--surface-*`, ink through the `--d*` ramp,
  hairlines and hovers through `--w*`, shadow ink through `--shc-*`, and tints through the `-rgb`
  companions (`rgba(var(--ok-rgb), .1)`). A literal is a value that cannot be themed.
- Both themes are audited against **composited** backgrounds, not nominal ones, across all
  ~16,750 rendered elements:

  | Theme | Items under target | Worst | Under 3:1 |
  |---|---|---|---|
  | Light | 6 | 3.40:1 | **0** |
  | Dark | 85 | 2.86:1 | 8 |

  Every one of the 8 dark items under 3:1 is `--qa-accent` set as text on `--qa-accent-dim`
  (2.86:1), and 44 of the 83 involve that token — it is the **placeholder** borrowed from Talent,
  and it is the single change that would clear them. For comparison the previous commit measured
  62 items, worst 1.87:1, 10 under 3:1 across 40% fewer elements, so both the worst case and the
  sub-3:1 count improved while the library grew.
- The contrast table in `index.html` measures itself from the live token values and recomputes on
  switch, so it cannot drift from the theme it documents.

### Recovered after the colour pass

An in-progress colour edit dropped a large part of the library from `index.html` before it was
committed. It was recovered from the last commit and re-expressed in the **current** token layer,
so the components and the new colours arrive together on the next `aimy-ds.css` extract.

| What was lost | Scale | Evidence it was still needed |
|---|---|---|
| Component CSS | **460 classes** | All 460 are referenced by Knowledge and/or Sales today |
| Component documentation | **91 sections** | Forms, tabs, tables, overlays, AI components, Knowledge v2 primitives |
| Typography token layer | **29 tokens** | `--fs-*` `--fw-*` `--lh-*` `--ls-*` `--fst-*` — §2 documents all of them; both products ship them |
| The nine `.ds-`-prefixed components | `ds-tabs` `ds-switch` `ds-choice` `ds-range` `ds-progress` `ds-field` `ds-textarea` `ds-kbd` `ds-divider` | Exactly the failure both `aimy-ds.css` headers warn about: *"the drop list is by banner section, never by `.ds-` prefix: nine real components carry that prefix and a prefix strip deletes them."* |

Only **8** of the 468 dropped classes were genuinely unused, and going the other way only ~20
classes now in the system are unused by either product — most of them documentation-site chrome
(`ds-code-label`, `ds-copy-btn`, `aimy-overlay-demo`) rather than dead components. The library was
not carrying significant cruft; it was missing most of itself.

Four tokens were also referenced but never defined anywhere — `--transition-fast`,
`--transition-base`, `--motion-hover-lift-sm/-md` — so every transition and hover lift reading them
silently did nothing. They are now defined as the aliases they were plainly meant to be.

**Renamed during recovery.** HEAD's vocabulary was mapped onto the current one rather than
reintroduced: `--accent*` → `--qa-accent*`, `--ai-text` → `--ai-ink`, `--hairline` → `--w07`,
`--teal-label` → `--cyan-label`. `--font-display` was folded into `--font-sans` here when Poppins was the display face and Urbanist the primary; §2 has since made Poppins the only face, so both tokens are defined again and both name it.
62 per-component `[data-theme="light"]` overrides came back with the old light palette and were
**deleted, not ported** — every one only restated what the token layer already does, and keeping
them would have reintroduced the very values this pass replaced.

### Adopted back from the products

`Knowledge/GAPS.md` (39 findings) and `Sales/old/GAPS.md` are gap registers written
**for the design-system owner**: places where a product had to work around the library.
Where both products independently built the same missing layer, the library is the thing
at fault, and that layer has now been brought in here — translated into this system's
vocabulary (px, `--qa-accent-rgb`, `--ai-ink`, `--w07`), not copied from either product's.

| Adopted | Was | Source |
|---|---|---|
| **Press feedback** — `:active` on 20 controls at `scale(0.97)`, large surfaces at `scale(0.995)`, transitioned on `--t-press` | `translateY(1px)` on three classes; `--t-press` defined and **used by nothing** | GAPS §1.9. Both products built it; QA had built it before them. *"Two products inventing the same missing layer."* |
| **Pointer targets** — WCAG 2.2 SC 2.5.8, 24×24 minimum via `::after` and `min-height` | controls drawing at 16–23px tall | Both products. Hit area grows, drawn size does not — the criterion is about the target, not the ink |
| **Form-control reset** — `font-family: inherit` on form elements, `background: none` on button-rendered tabs, `strong/b` pinned to `--fw-extrabold` | nothing | GAPS. Most specimens here are `<div>`s, so the omission never surfaced on this page; on real `<button>`s tabs rendered in the UA font over `buttonface` |
| **Entry stagger** — `.ds-stagger` / `.ds-enter`, 40ms per item capped at 8 | nothing | Shipped as `.k-stagger` in Knowledge and `.s-stagger` in Sales — same behaviour, two names. The neutral name lives here so they converge |
| **`.aimy-toast`** corrected to the spec its own anatomy table states | the CSS implemented a *different* toast: bottom-right, green success chip, column layout, horizontal divider, `--ok` fill over 4s | GAPS §1.10. All 8 documented rows diverged. Both products were overriding it locally |
| **Button heights** — explicit `line-height` on `.btn` / `-sm` / `-lg` | inherited, so the same class measured 29px in one container and 25px in another | GAPS §1.11 |

The toast was fixed **in place** rather than as an override layer: leaving the stale rules
next to the correct table is precisely the confusion §1.10 reports — *"Both are in the same
file, and only one is published."*

### Reconciled against GAPS.md and against the products as built

`Knowledge/GAPS.md` carries its own status table: twelve findings fixed on `close-gaps`, four
still needing a decision. That branch is an ancestor of `main`, so the twelve were **already in the
last commit** — and the colour pass then dropped some of them again, in the same way it dropped
`.search-field`: the rule survived while declarations inside it did not. `.btn` kept its rule and
lost its `line-height`.

Closed in this pass, each verified by measurement rather than by reading:

| § | What was wrong | Now |
|---|---|---|
| **1.11** | I had set `.btn` line-heights to 16/15/17, copying Knowledge's local override. GAPS' own correction names those exact values as wrong — they render **34/27/39** | **14/12/15**, rendering **32/24/37**, with **spread 0** measured across containers of line-height 1 and 2.6. Context-independent, which is the point of the finding |
| **1.2.1** | `.bcard` padding had drifted to 14 | 16, matching the library and *"settled at radius 16 / padding 16"* |
| **§2 Case** | `.tag` and 17 other label pills rendered in **capitals with `--ls-wide` tracking** — contradicting this document's own rule | Sentence case, tracking dropped in the same edit, exactly as §2 requires and as Sales ships. 51 **section markers** keep their capitals, which is the one role §2 says they belong to |
| **§2 floor** | *"Nothing is smaller than 12, and no product may lower it"* — recorded here as done in every product, while this file still had **732 sites** between 7px and 11.5px | All 732 raised. Smallest type outside a code sample is now 12px. Sales records the same move: *"Its type is 10.5–11.5px. On the scale here that is 12 and 13"* |
| **—** | `.filter-chip` had fallen to 12px | `--fs-xs`, matching the library and both products |

**Measured, not assumed.** The comparison was run by loading the design system, Sales and Knowledge
in the same browser and diffing computed styles on shared classes. That is what caught `.tag` at
10px in capitals and `.bcard` at 14 — none of which reads as wrong in source.

It also caught a distinction worth keeping: Sales' `.tc-title` renders 18px/800, but that is
`.b-qcard .tc-title`, a **product override**, not the library value. `aimy-ds.css` — the extracted
layer both products start from — ships 14px/700. Card type sizes were therefore left alone rather
than adopting a product's scoped decision as the system's.

### The four that were left, resolved

**§1.8 — the ramp had a collapsed rank, not a failing one.** Re-measured, dark already cleared AA
on every rung, so the original finding had been overtaken. What it left behind is the defect §1.8
warns about in its own remediation: *"raising a rung to fix its contrast moves it into its
neighbour … a legibility fix that deletes a rank is not a fix."* `--d500` and `--d600` sat at
**ΔE 1.15**, under the ~2.3 JND — two ranks rendering as one colour. Both are used **only** as
`color` (44 and 28 sites), so neither could be demoted to a non-text rule value.

Re-spaced along the existing hue so all three bottom rungs stay legible *and* stay distinct:

| rung | was | now | worst contrast | ΔE to next |
|---|---|---|---|---|
| `--d400` | `#93a2b4` | `#95a4b5` | 6.03 | 4.86 |
| `--d500` | `#8394a8` | `#8898ac` | 5.21 | 4.15 |
| `--d600` | `#8091a5` | `#7c8ea4` | 4.57 | — |

Every dark rung now clears AA (worst 4.57) and every adjacent pair clears the JND. §7's AA claim
stands without qualification, which was the choice §1.8 asked for.

**§1.1 — built.** Doctrine §6.2 bound "explain what AiMY detected" to `.context-zone` and
"prioritised recommendations" to `.v2-chip`; both resolved to an anchor and to no CSS, so the
binding pointed at classes that drew nothing. Both families are now implemented from their own
anatomy tables — `.aimy-context-panel`, `.context-zone` and its `--state` / `--suggestions`
variants, the state pill and its alternates, and the three-tier chip with severity on four channels
(border tint, ground tint, a 2px **top** edge, and a badge) rather than on colour alone.

**§1.3 — built.** Sixteen chart primitives documented and none implemented: `.v2-header` and its
rows, `.v2-title` / `.v2-subtitle`, `.v2-controls`, `.range-tabs` / `.range-tab`,
`.compare-toggle`, `.v2-stats-row` and the `.v2-stat*` family, `.v2-legend`, `.legend-item`,
`.legend-line` (with a dashed variant, so a second series states itself as dashes rather than as a
second hue), plus `.anno-dot` and `.anno-line`.

All three sections now **demonstrate their classes instead of mocking them up**: 9,569 characters
and 51 inline `style` attributes of hand-drawn specimen replaced by markup that uses the
components. That was §1's actual complaint — *"the specimens that appear to demonstrate them are
inline-styled, so the page looks complete while the classes it documents do not exist."*

Sizes were raised to the 12px floor on the way in: the anatomy tables were written against the old
scale and name 9–11px in several rows.

**§4 — nothing to build here.** GAPS says so itself: *"Not a design-system defect; a tension inside
`AiMY_Knowledge_v2_Design_Direction.md`."* §9.2 budgets seven to nine blocks from §10.3's declared
nine, four of which are owner-only — so for an owner the inventory and the budget are the same set
and composition never chooses, while a pure consumer cannot meet the budget at all. The machinery
is correct; the inventory needs to be roughly double the budget before per-user composition means
anything. **That is a product ruling, and it is still open.**

### Components that rendered as raw browser controls

The search field and the textarea were drawing as unstyled UA inputs — a white box with an inset
border on a dark page. The cause is a failure mode a class-level check cannot see: **the colour
pass removed base rules while leaving state rules behind.** `.search-field` kept only
`.search-field.is-focus`; `.ds-textarea` kept only `.ds-textarea.is-error`. The class was still
"present", so the earlier recovery pass — which compared class names — reported nothing missing.

Re-running the comparison at **rule** level (selector by selector against the last commit) found
186 lost rules, 155 of them matching live markup. Of those, ~130 were the per-component
`[data-theme="light"]` overrides deliberately dropped earlier, leaving **21 genuine base rules**,
now restored and re-expressed in current tokens:

`.search-field` · `:focus-within` · ` svg` · ` input` · ` input::placeholder` — `.ds-textarea` ·
`:focus` · `::placeholder` — `.ds-progress` — `.pop` — `.priority-badge.p1/.p2/.p3` —
`.ds-preview` demo scoping (7) — `.token-item > *` / `.grad-item > *`

Two needed correcting rather than restoring verbatim. `.ds-progress` took its track from
`--card-bg-raised`, which is `#ffffff` in light — a white track on a white card; a track has to
read on **any** surface, so it is a wash now. And the recovered `.ds-theme-toggle svg` belonged to
the previous toggle; this file's toggle sizes its own icons.

### Containers whose children were styled and which had no rule themselves

Five more were found by asking the browser which specimen elements no class rule matches at all.
Each had fully-styled children and nothing on the container, so it rendered as a stack of correct
parts in the wrong shape — `.agent-header-info` already declared `flex:1`, `.goal-mini` was
already a card, `.coaching-card-header` already drew its own divider.

| Component | Rendered as | Now |
|---|---|---|
| `.agent-header` | avatar, info and actions stacked vertically | a row |
| `.goal-six-grid` | six cards in one column, 533px tall | an auto-fit grid |
| `.coaching-card` | a "card" with no surface, border or radius | a card |
| `.driver-icon` | — | a sized inline box (it was only 0×0 because its section is collapsed) |
| `.kf-score-ok/-warn/-err` | plain strong text — named for a verdict, showing none | the semantic colour |

`.field-help` gained a standalone base rule (the line is not always inside a `.ds-field`) plus a
`.is-error` / `.is-success` modifier, and three specimens that faked it with
`style="color:var(--err)…"` now use the class — inline-styled specimens are what let a component
look implemented while having no CSS, which is the whole subject of GAPS §1.

**Still open:** 589 classes named in anatomy tables have no CSS, against 8 before this pass that
were also *used* in a live specimen. Almost all of the 589 belong to the newer QA sections
(`eval-*`, `editor-*`, `kdo-*`, `goal-*`, `v2-chip-*`, `cd-*`, `di-*`, `memory-*`), whose specimens
are inline-styled: the page looks complete while the classes it documents do not exist. Only 3 of
them exist in either product, so this cannot be recovered from Knowledge or Sales — it has to be
built or the tables corrected.

### Structure — the specimens now sit on the elements the products build them with

A specimen is not just a picture of a component; it is the contract for how to compose one.
Most of these were `<div>`s, and a component only ever exercised on a `<div>` silently depends on
whatever the UA supplies the moment it is used on the element it *should* be used on.

| Component | Was | Now | Why |
|---|---|---|---|
| `.type-card` | `<div>` | `<article>` | A self-contained item in a list. Sales composes its queue card as `<article class="type-card s-card b-qcard">` — the library card **is** the base, with product classes layered on |
| `.tc-title` | `<div>` | `<button type="button">` | The title is the card's affordance — it opens the record. Needed `display:block; width:100%; text-align:left` to survive, since a button centres and shrink-wraps |
| `.tc-summary` | `<div>` | `<p>` | Both products agree |
| `.tab` | `<div>` | `<button role="tab" aria-selected>` | A tab strip is interactive; on a `<div>` it is not focusable, not reachable by keyboard, and announces as nothing |
| `.chip` | `<div>` | `<button type="button">` | Sales builds chips as buttons |
| `.menu-item` | `<div>` | `<button type="button">` | Already carried `role="menuitem"` while being unfocusable |

That change is only safe because of the base reset adopted with it — the one both products ship
**byte-identical**:

```css
button { background: none; border: 0; padding: 0; font: inherit; color: inherit; appearance: none; }
```

At element specificity (0,0,1) every component class still wins. Measured across all 68
button-bearing classes on this page: 15 moved, and all 15 were components that had never declared
a value and were inheriting the UA's button default. Three of them measured their *height* from it
(`.cite-action`, `.td-action`, `.dv-notice-link`) and are now pinned to `--lh-tight` — the same
class of defect as §1.11, found by the same reset. Verified after: `.tab` on a `<button>` renders
transparent in Poppins instead of a light grey chip in the UA font, and `.link` loses the 2px UA
border it never wanted. 22 specimens are keyboard-reachable that were not.

`data-select-sibling` now syncs `aria-selected` and the roving tabindex alongside `.active`. A
`role="tab"` whose `aria-selected` still names the old tab tells a screen reader the inverse of the
truth, which is worse than shipping no ARIA at all (GAPS §1.7; `dsTab()` already did this).

### Not adopted, and why

- **Knowledge's `.type-card` / `.tc-*`** — the newer card is written against Knowledge's own
  `--ty-*` type scale, `--ink-faint`, `--hairline` and `rem` units against a fluid root. That
  is the divergence §9 of this document exists to remove, so importing it would import the
  drift. The portable parts (line-clamping, `text-wrap: pretty`, a quiet pill type badge) are
  worth taking, but each needs re-expressing in this system's tokens first.
- **Shell and layout overrides** (`.aimy-overlay`, `.aimy-float-wrap` moving to `position:
  fixed`) — product app-shell positioning. The specimens here are `absolute` inside a preview
  box on purpose.
- **`.ds-theme-toggle`** — both products override it, but against the older toggle; this
  file's is newer.

### Still open

Roughly 290 design-system classes are redefined by one product or the other. Most are local
layout, but the registers name structural gaps this pass did not close — among them: no overlay
primitive between `.aimy-overlay` and `.modal` (GAPS addendum); `.ai-insight-panel` bound by
doctrine §6.2 to a class that draws nothing (§1.1); `.copy-field` embedding `.copy-btn`, which
products drop as documentation chrome (§1.12); and nine components found drawn at specimen
scale rather than product scale (§27, §30, §37, §39).

---

## 5. Component inventory

### Components (base)
| Component | Classes | Notes |
|---|---|---|
| Buttons | `.btn` + `.btn-brand/ghost/err/warn/ok/accent`, `.btn-sm/.btn-lg` | Contextual color; 13/700; radius `--r-md`. **A control, never a label:** a hairline border and no ground, except the one filled primary per surface |
| Tags & badges | `.tag` + `tag-ok/warn/err/info/teal/ai/accent/neutral`, `.signal-badge` | **A label, never a control.** One ground and a transparent border for every tone; uppercase 700 at `--fs-2xs` / `--ls-wide` in a 16px line box. Only `tag-ok` and `tag-err` colour the word and add a 15% tint of their own hue — the rest are identical to `tag-neutral` by design. Never give it a visible border: that is what a control wears |
| Chips & filters | `.chip` (`default/active/brand/ok/warn/err`), `.afs` strip | Active = accent |
| Dropdown | `.v2-dropdown` + `-btn`/`-panel`/`-option`, `.dd-label-text` | **The only select control.** Custom listbox: full keyboard model, typeahead, focus return, `aria-haspopup="listbox"` / `role="listbox"` / `aria-selected`. Never use a native `<select>`, and never rebuild this pattern by hand |
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
Field & states `.ds-field/.field-input` (`.is-error/.is-success` + `.field-help`) · Select → use `.v2-dropdown` (+ `.roster-dd` full-width, `.is-error`); label it with `aria-labelledby` and add `input[type=hidden]` to post a value · Search `.search-field` · Textarea `.ds-textarea` (+ `.is-error`) · Date picker `.cal` (today outlined, selected accent) · Radio cards `.radio-cards/.radio-card` (`:has()`) · Stepper `.stepper` · File upload `.uploader` · Tag input `.tag-input/.tag-token` (+ `.is-error`) · Password `.pw-wrap/.pw-eye/.pw-meter` (weak/mid/good) · OTP `.otp` (+ `.is-error`) · Time picker `.time-picker/.time-panel/.time-opt` · Input group `.input-group/.ig-addon` · Copy field `.copy-field` · Dual range `.drange` · Upload progress `.upload-list/.upload-item` (uploading/done/error) · Error summary `.form-summary` (`role="alert"`, links to fields)

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

### AiMY Doctrine Primitives

Components required by the **Knowledge-to-Action Doctrine**. These are not optional garnish — the doctrine's review gate fails a surface that omits them (see §9).

| Component | Classes | Anchor | Doctrine rule |
|---|---|---|---|
| **Work state** | `.work-state` + `.ws-detected/-recommended/-drafted/-staged/-completed/-failed`, `.ws-dot`; pipeline `.ws-track/.ws-step(.is-past/.is-current)/.ws-sep` | `#work-state` | §2.3 — a **required field** on every surfaced item. Canonical value lives on `data-work-state`; `handled`/`blocked` are display aliases for `completed`/`failed` only. **Four of the six are positions, not verdicts:** detected · recommended · drafted · staged all take the plain pill, and only `completed` and `failed` carry a hue. What separates the four is the **dot** — hollow while AiMY is still working on it, filled once the thing is real. On the pipeline, the current step is carried by ink at the top of the ramp, not by a hue |
| **Confidence badge** | `.conf-badge` + `.conf-high/-medium/-low`, `.conf-meter`, `.conf-val` | `#sc-conf-badge` | §5.7, Level 5 — show where confidence changes interpretation. Medium and low must also state *what limits them* |
| **Briefing card (extended)** | `.bcard-ack-row`, `.bcard-ack-btn(.is-acked)`, `.bcard-dismiss-picker(.open)`, `.bcard-dismiss-reason` | `#bcard-extended` | §5.9 — every item is dismissible with a captured reason; reversible dismissals offer Undo |
| **Entry modes** | `.entry-action` + `.em-direct/-investigate/-prompt/-review`, `.em-ico`; spec tag `.entry-mode-tag` | `#entry-modes` | §3 — classification is **mandatory and explicit** at design time. An unclassified action fails review |
| **Memory panel** | `.memory-panel`, `.mem-head/.mem-age/.mem-thread/.mem-line/.mem-who/.mem-what/.mem-foot` | `#sc-memory-panel` | §4 continuity — shows what is carried forward and lets the user drop it |
| **Governance change request** | `.gov-cr-card`, `.gov-cr-head/-title/-diff/-current/-proposed/-label/-val/-arrow/-rationale/-blast/-actions` | `#kpihub-cr-card` | §3.1 rung 3 — governed config changes get a diff, a rationale, a blast radius, and an audit note |
| **Decision zone** | `.decision-zone`, `.dz-prompt/.dz-consequence/.dz-actions/.dz-spacer/.dz-meta` | `#disputes-decision` | §3 — **Accept · Edit · Reject**. Edit is not optional |
| **Audit trail** | `.audit-trail`, `.audit-entry(.is-ok/.is-warn/.is-err/.is-ai)`, `.audit-ico/-main/-action/-actor/-who/-side/-time`, `.audit-revert`, `.audit-irreversible` | `#disputes-audit` | Level 6 — every entry names actor, action, time, and reversibility. AiMY's own actions are never disguised as the user's |
| **Modal + wizard** | `.modal` + `.steps/.step(.done/.active)` + carried `.ctx-chips` | `#disputes-modal` | §7.2 — the structured destination. The canvas does not replace workflows that need ordered inputs or a durable record |
| **AI unavailable** | `.ai-unavailable(.is-degraded)`, `.aiu-mark/-title/-body/-fallback/-note` | `#ai-unavailable` | §6.7, Level 7 — a designed state. Must say **what still works** and never lose staged work to an outage |
| **Confirmation ladder** | documentation table (binds rungs to existing components) | `#confirmation-ladder` | §3.1 — confirmation is proportional to consequence; the ladder runs one way only |

### Knowledge v2 Primitives

Built for **AiMY Knowledge v2** (`AiMY_Knowledge_v2_Design_Direction.md`), but none of them are Knowledge-specific — trust state in particular is a shared primitive precisely because it has to render inside other agents' surfaces.

| Component | Classes | Anchor | Requirement |
|---|---|---|---|
| **Trust state** | `.trust-state` + `.ts-verified/-due/-expired/-unverified/-superseded`, `.is-excluded`, `data-trust-state`; `.trust-line` | `#trust-state` | Knowledge §6.2 (D1) — required on every knowledge object. **A second axis, independent of work state**: an object can be `drafted` and `expired` at once. Uses semantic tokens only, **never `--accent`**, so it reads identically when cited inside a re-themed host surface |
| **Answer trust disclosure** | `.trust-disclosure(.has-exclusion)`, `.td-row(.is-ok/.is-warn/.is-err)`, `.td-text`, `.td-action` | `#trust-disclosure` | Knowledge §7.4 — every answer states its grounding. The exclusion case must never be silent, or a governance gap is indistinguishable from a corpus gap |
| **Citation preview** | `.cite-wrap`, `.cite-preview(.is-open)`, `.cp-head/-title/-passage/-foot/-src`, `.cite-action(.is-flag/.is-flagged)`, `.cite.is-flagged/.is-excluded` | `#cite-preview` | Knowledge §7.3, §7.5 (D2) — verification rung 3, the one carrying the most traffic. Opens on hover **and** `:focus-within`; feedback is captured **per citation**, not per answer |
| **Set-scope operations** | `.set-scope-bar`, `.ss-count/-num/-scope/-actions/-clear`, `.ss-preview`, `.ss-effect(.is-ok/.is-warn/.is-skip)` | `#set-scope` | Knowledge §4 (D3) — bulk work over a filtered collection. The scope statement and the skip line are both mandatory: a bulk op that silently no-ops on part of its selection reports success the user has no reason to distrust |
| **Aggregate briefing card** | `.bcard.is-aggregate`, `.agg-summary/-stat`, `.agg-list/-row/-label/-val/-bar/-more` | `#bcard-aggregate` | Knowledge §10.3 blocks 3 and 7 (D4) — a briefing item whose subject is a cluster, not a record. `.agg-more` is required when the list is truncated, or a broad problem reads as a narrow one |
| **Type cards** | `.type-card(.is-compact)`, `.tc-head/-type/-title/-summary/-body/-fields/-list(.is-negative)/-quote/-tags/-gov/-action`, `.tc-approval(.is-approved/.is-pending/.is-internal)` | `#type-cards` | Knowledge §6.3 (G1) — eight templates over one **fixed governance row**. Type by icon + label, never colour. `.is-compact` is the embedded form required by §8.1 |
| **Document viewer** | `.doc-view`, `.dv-head/-meta/-title/-gov/-gov-item/-notice/-body/-rel/-rel-item/-actions` | `#doc-view` | Knowledge §6.4 (G2) — trust state **above the body** in a fixed position. Carries the relationship set (related · superseded-by · contradicts) named in §6.1 but absent from the library |
| **Version history & restore** | `.ver-list/.ver-item(.is-current/.is-ai)`, `.ver-mark/-label/-author/-time/-tag`, `.ver-compare/.vc-*`, `.ver-restore/.vr-effect` | `#version-history` | Knowledge §6.5 (G3) — AI edits are **ordinary versions with an AI author**, never a parallel history. Restore is a commit surface stating its effect, and is additive |

---

## 6. States

Every interactive component documents its states statically (for Figma capture) via helper classes that mirror the real pseudo-states:

- `.is-hover` / `.is-active` / `.is-focus` — mirrors `:hover` / `:active` / `:focus-visible`
- `.open` / `.visible` / `.selected` / `.is-open` — forced-open overlays
- Coverage: buttons (5 states), inputs (default/focus/error/success/disabled), selection controls, nav/tabs/chips, all overlays open (menu, popover, confirm, tooltip, drawer, modal), row components (tree/notification/palette/time), error variants (select, textarea, tag input, OTP), strength meter, upload statuses.

---

## 7. Accessibility

- WCAG 2.1 AA target; both themes audited against composited backgrounds. Light has nothing
  below 3:1; dark has 8 items at 2.86:1, all of them `--qa-accent` on its own tint. See §4.
- Focus: `:focus-visible` only, 2px `--brand` outline, 2px offset. Never remove without replacement; never use the accent for focus.
- Native elements first: `<details>` accordions/trees, native checkbox/radio/range where possible. **Select is the deliberate exception** — `.v2-dropdown` is a custom listbox chosen for cross-platform visual consistency, and it therefore carries its own keyboard model, focus management and ARIA (§10.3).
- `prefers-reduced-motion: reduce` disables shimmer, pulses, spinners, lifts.
- Error summaries use `role="alert"` and receive focus on submit; every error state pairs color with text.
- Mask sensitive fields (API keys, passwords) by default.

---

## 8. Files

| File | Purpose |
|---|---|
| `index.html` | The design system — tokens, components, states, themes, live demos |
| `design-system.md` | This reference |
| `00_AiMY_Knowledge_to_Action_Doctrine.md` | Interaction doctrine — owns *behaviour*, not tokens or component anatomy |

> **Naming note.** The doctrine refers to the component library as **`design-doc.html`**. In this repository that file is **`index.html`** — the two names denote the same artefact. Every `design-doc.html` anchor cited in the doctrine resolves against `index.html`.

---

## 9. Doctrine binding

The doctrine's §0 binding rule: *"Where this document names a component, that name must resolve to an entry in `design-doc.html`."* Every §6.2 responsibility now resolves:

| Doctrine responsibility | Primitive | Anchor |
|---|---|---|
| Operational metrics and status | Cards, Badges & Status, Chart Primitives, AiMY Badge | `#cards` · `#badges` · `#chart-primitives` · `#canvas-badge` |
| Briefing item, full anatomy | Briefing Card — Extended | `#bcard-extended` |
| AI interpretation within a briefing | AiMY Insight Panel · Chart Annotations · Memory Panel | `#ai-insight-panel` · `#anno-card` · `#sc-memory-panel` |
| Prioritised recommendations | AiMY Action Chips | `#v2-chip` |
| Ambient conversational entry | Float Input Bar · Filter Tray | `#canvas-float` · `#canvas-filter-tray` |
| Explain what AiMY detected | Context Zone | `#context-zone` |
| Hold the active conversation | Canvas Overlay · Chat Messages | `#canvas-overlay` · `#canvas-messages` |
| Govern consequential changes | Governance Change Request · Decision Zone · Audit Trail · Modal + Wizard | `#kpihub-cr-card` · `#disputes-decision` · `#disputes-audit` · `#disputes-modal` |
| Confidence disclosure | Confidence Badge | `#sc-conf-badge` |
| Reversible / completed work | AiMY Toast with `.aimy-toast-undo` | `#canvas-toast` |
| Empty, loading, unavailable | Empty & Loading States · AI Unavailable | `#states` · `#ai-unavailable` |
| Declare AI work state (§2.3) | Work State | `#work-state` |
| Classify actions (§3) | Entry Modes | `#entry-modes` |
| Proportional confirmation (§3.1) | Confirmation Ladder | `#confirmation-ladder` |

---

## 10. Doctrine gap register

Discrepancies between the doctrine text and the implemented library, recorded for the doctrine owner.

### 10.1 §6.3 gaps that were already closed

The doctrine listed five primitives as "missing — do not improvise". All five existed in the library at the time of the audit; the doctrine was stale, not the implementation.

| Cited as missing | Actually implemented at | Classes |
|---|---|---|
| Suggestion Review | `#ai-suggestion` | `.ai-suggestion` with `del`/`ins` diff, Accept / Reject / Edit |
| Type-to-Confirm | `#confirm-destructive` | Modal + gated destructive button |
| Context Chips | `#context-chips` | `.ctx-chips` / `.ctx-chip`, removable |
| Stat Card | `#stat-card` | `.stat-card`, `.stat-delta.up/.down` |
| Response Actions | `#ai-actions` | Copy / regenerate / thumbs |

**Note on Suggestion Review vs. Governance Change Request.** They are not duplicates. `.ai-suggestion` handles message-level edits; `.gov-cr-card` handles governed configuration, where a rationale, a blast radius and an audit note are required. Use the lighter one unless the change touches governed config.

### 10.2 `--d200` — the doctrine's claim is incorrect

The doctrine's "Open scale flag" states `--d200` is undefined in the dark scale and that `fill: var(--d200)` silently falls back to black, and §11 accordingly bans the token. **This is false.** `--d200` is defined in both themes and is a documented step of the neutral ramp (§1):

| | Value | Defined at |
|---|---|---|
| Dark | `#c3ceda` | `:root` in `index.html` |
| Light | `#2e3747` | `:root[data-theme="light"]` in `index.html` |

`--d200` is safe to use. The ban should be lifted.

### 10.3 `<select>` — resolved in favour of the custom dropdown

The doctrine's Level 3 said *"No native `<select>` — use `.v2-dropdown`"*, while this system's accessibility policy (§7) said *native elements first* and shipped `.ds-select`, a styled native select. Two components claimed the same job.

**Resolved: `.v2-dropdown` is the system's only select control.** `.ds-select` and every native `<select>` have been removed; there are now zero `<select>` elements in the library.

The audit also found that `.v2-dropdown` was a **phantom component** — its anatomy table and code sample documented `.v2-dropdown-btn`, `.v2-dropdown-panel`, `.v2-dropdown-option` and `.dd-label-text`, but none of those classes had CSS and the control had no behaviour at all; the specimen was an inline-styled mockup. The doctrine's Level 3 rule pointed at something that did not exist. It has now been built:

| Supplied | Detail |
|---|---|
| Styling | Classes match the previously documented anatomy exactly; the original specimen's visual is unchanged |
| States | default · hover · focus-visible · open · selected · keyboard-active · disabled · error · full-width (`.roster-dd`) |
| Keyboard | ↓/↑ open and move · Enter/Space select · Home/End · Esc closes and returns focus · Tab closes · letter typeahead (500ms buffer) |
| ARIA | `aria-haspopup="listbox"` + `aria-expanded` on the trigger; `role="listbox"` + `aria-activedescendant` on the panel; `role="option"` + `aria-selected` on rows. Missing attributes are normalised at load |
| Forms | Optional `input[type=hidden]` receives the value and fires `change`; the wrapper emits a bubbling `dd:change` |
| Light mode | Panel, hovers and selection tints all flip |

**The tradeoff is now explicit rather than implicit.** A custom listbox gives one appearance on every platform at the cost of re-implementing what the browser used to provide — keyboard, focus, and screen-reader semantics. That work lives in this one component, which is exactly why products must use it rather than rebuild the pattern: a hand-rolled copy will look right and be unusable without a mouse.

### 10.4 Gate violations found and fixed in the library

Found while closing the gaps above; all were pre-existing.

| Violation | Count | Gate | Fix |
|---|---|---|---|
| `prefers-reduced-motion` documented as a code sample but **never implemented** | — | L4 + L7 | Real `@media (prefers-reduced-motion: reduce)` block added. Motion that carries meaning (spinners, the toast timer) is frozen rather than removed, so the signal survives |
| `transition: all` | 12 | L4 | Replaced with explicit property lists |
| `onclick=""` string attributes | 116 | L4 | Converted to `data-*` attributes with a single delegated listener. Beyond tidiness: inline handlers are blocked by a strict CSP, so markup copied from this page could not previously ship into a CSP-enforcing product |
| Toast progress bar animating `width` | 1 | L4 | Now `transform: scaleX()` with `transform-origin: left` |
| `onmouseover`/`onmouseout` inline style writes | 3 | L4 | Replaced with CSS `:hover` (`.icon-btn`, `.lift-demo`) |
| Native `<select>` elements | 7 | L3 | All migrated to `.v2-dropdown`; `.ds-select` retired. Zero `<select>` elements remain |
| Duplicated `<!-- END MAIN -->` comment | 1 | — | Removed |
| Light-mode neutral fill flattening semantic tints on `.conf-badge` and `.audit-ico` | 2 | L1 | Light override scoped with `:not()` so level and status modifiers keep their tint |
| `.progress-bar-fill` animating `width` at **600ms** | 1 | L4 | Now `transform: scaleX(var(--fill))` with `transform-origin: left`, 300ms. **Breaking change** — set the level with `--fill` (0–1), not `style="width:%"`. The five in-page usages and the code sample were migrated |
| `.score-ring-fill` transitioning `stroke-dashoffset` at **800ms** | 1 | L4 | Reduced to `--t-slow` (300ms). `stroke-dashoffset` is retained — it is the only way to draw an SVG arc — but the ceiling still applies |
| `.ds-switch .thumb` animating `left` | 1 | L4 | Now `transform: translateX()`; `left` relayouts, `transform` composites |
| Inline `onkeydown=""` on the canvas textarea | 1 | L4 | Missed by the first sweep, which matched `onclick` only. Now `data-submit-on-enter` + a delegated `keydown` listener. **Zero inline event handlers of any kind remain** |

### 10.5 Still open

- **Canonical 7-level framework reconciliation** — the doctrine's §8 notes its gate is codified locally and should be reconciled with any canonical FlairsTech definition.

### 10.6 AiMY Knowledge v2 — open dependency register

Against `AiMY_Knowledge_v2_Design_Direction.md` §12. Every component binding in that document's §9.4 resolved on audit **except trust state**, which the document itself flagged.

| Dep | Status | Resolution |
|---|---|---|
| **D1 — Trust state primitive**<br>*blocks the card design and the briefing* | ✅ **Built** | `#trust-state` — five values, `data-trust-state`, `.is-excluded` for the retrieval consequence. Built as a **shared** primitive with semantic tokens only and no `--accent` dependency, per Knowledge §1.1/§8.1. The §7.4 answer-level disclosure ships alongside it at `#trust-disclosure` — it was an unnumbered requirement with no component |
| **D2 — Citation hover preview + per-citation feedback**<br>*blocks the answer surface* | ✅ **Built** | `#cite-preview` — the intermediate verification rung. Rungs 1 (`.cite`) and 2 (`.source-list`) already existed; rung 4 is navigation. Preview opens on hover **and** focus, and per-citation flagging routes into the correction loop rather than terminating in a rating |
| **D3 — Set-scope AI operations**<br>*blocks Library bulk curation* | ✅ **Built** | `#set-scope` — selection bar with a mandatory scope statement, effect preview including skips, and explicit binding to the confirmation ladder rungs |
| **D4 — Coverage-gap block shape** | ✅ **Built** | `#bcard-aggregate` — resolved as a `.bcard` variant, as the document anticipated. Same meta row, conclusion, action row and ack/dismiss row; only the evidence zone changes |
| **D5 — Ownership and usage data granularity** | ⬜ **Not a design-system dependency** | Platform data availability. The design system supplies the blocks; whether composition can rank them per user is a data question. If it degrades to entitlement-only, no component changes — the briefing simply renders a shorter set, and `#states` covers the honest empty case |
| **D6 — Permission-aware retrieval** | ⬜ **Not a design-system dependency** | Retrieval-layer capability. It does carry one design obligation: where the guarantee does not hold, the limitation must be stated on-screen. Bind that to `.banner.warn` or `.inline-note.warn`, and use `#trust-disclosure` on answers — both exist |

**Not blockers, but worth stating:** the direction document's §7.1 (one input routed on intent) and §7.2 (scope before query) need no new components — `.search-field`, `.cmdk`, `.aimy-float-bar` and `.filter-tray`/`.filter-chip` cover them. §8's embedded-service contract is a *constraint on usage*, not a component: it is satisfied by the answer-surface components carrying no shell dependency, which is why trust state was built accent-free.

### 10.7 Knowledge v2 — §12.1 component gaps

Second audit, against the revised direction document. Its three declared gaps were confirmed absent and are now built. Its claim that *"everything else resolves today"* was checked item by item and holds, with the two exceptions noted below.

| Gap | Status | Resolution |
|---|---|---|
| **G1 — Eight type card templates**<br>*blocks the workbench, the viewer, and embedded citations* | ✅ **Built** | `#type-cards`. Article · Ticket · ICP · Campaign · Marketing Asset · Success Story · Blog · Web Page, each with a distinct body zone over an identical governance row. `.is-compact` supplies the §8.1 embedded form — title, type, trust, one action |
| **G2 — Document viewer shell**<br>*blocks the viewer* | ✅ **Built** | `#doc-view`. Composes existing primitives into a reading shell: trust in a fixed position above the body, constant governance chrome, type-appropriate body slot, and exclusion / supersession notices that state the consequence **and** the route out of it |
| **G3 — Version comparison and restore**<br>*blocks the editor* | ✅ **Built** | `#version-history`. Single history with AI-authored versions marked rather than segregated, `del`/`ins` comparison reusing the suggestion-review diff shape, and restore as a commit surface stating rollback, downstream effect, and that history is preserved |

**Found in the audit but not listed as a gap.** The object anatomy in §6.1 names a **relationships** set — related objects, superseded-by, contradicts — with no component anywhere in the library, and §6.4 depends on it ("a superseded object resolves to its successor with the relationship stated"). Built as part of G2: `.dv-rel` / `.dv-rel-item`, with `.is-contradiction` reading as a finding rather than a neighbour, and `.is-successor` as the way forward.

**Judgement calls, flagged rather than decided:**

- **Approval state is kept out of trust state.** §12.2 asks whether approval becomes a sixth trust value or stays a separate field. `.tc-approval` is therefore built *outside* `.trust-state` — the conservative choice, since folding it in now would pre-empt the ruling and change a primitive that ships into other agents' surfaces. If the ruling makes it a trust value, the field folds in and the eight templates are unaffected.
- **Retrieval results (§7.1) and displacement notices (§10.3) have no dedicated component.** Both are compositions of existing parts — `.list-group` or `.cmdk` for a ranked result set, `.inline-note` / `.banner` for a displacement statement. Neither was declared a gap and neither needs a new primitive, but neither has a worked reference either. Raise one if the composition proves non-obvious in build.

### 10.8 Closed since the audit

- **`--qa-accent`** — withdrawn. Accents are **global**: one `--accent` token re-themed per product (§1). There is no QA-specific accent token, so there was nothing to swap and no Talent collision to resolve. The doctrine's open flag has been retracted.

---

## 11. The label, type and colour sweep — September 2026

Sections 1 and 2 state the rules. This section records what was actually changed to make the code
agree with them, so the next person can tell a deliberate exception from a site that was missed.

### What started it

A sales lead looked at a status column and said it looked like **traffic lights**. It did. The
system was carrying `#17b26a`, `#f79009` and `#f04438` — a green, an amber and a red at full
strength — and every tag wore a tinted ground *and* a border in the same hue, under full capitals.
Four amplifiers, applied together, to a component that appears eight times on a screen.

Colour was also being spent on the wrong thing. A count across the products found roughly **7,500
references to the three status hues**, with `--err` at 1,414 and `--ok` at 1,087 — both ahead of
`--brand` at 942. The loudest colours in the system were the most common ones.

### What changed

**The hues.** Three signals at roughly 75% saturation became a **family of six** at 22–49%
saturation and 59–66% lightness, reading 5.96–7.47:1 on the card. `--err` keeps about twenty
points more chroma than its siblings, deliberately, so a verdict still arrives first.

**The alarm.** `--err` had been carrying both a verdict and a control. `--err-strong` (#f04438 in
dark, #d92d20 in light) was added **outside** the family for one thing only: a control that stops
something already in flight. The muted red on an End-call button read as a suggestion.

**The pill.** Every tone brought its own tinted ground *and* its own border. Now there is one
ground — `color-mix(in srgb, var(--hue) 15%, transparent)` — and no border at all, because a
bordered capsule is the same object as a ghost button.

**The case.** `text-transform: uppercase` with `--ls-wide` became sentence case, with both words
capitalised when there are exactly two. The tracking left with the capitals that asked for it.

**The ink.** `--d300` through `--d700` were all being used for type. An **ink band** now says which
values may: `--ink-primary`, `--ink-secondary` and `--ink-muted`, with `--ink-placeholder` as the
single exception and `--ink-rule` and below reserved for non-text.

**The scale.** Four steps sat under 14 with body at 13, and 13, 15 and 17 were all in circulation
across four separate scales. Even steps only now, floor 12, body 16, and the four scales
reconciled.

### Where it was applied

Three repositories, one pass: **design-system** (`index.html`, this document), **Sales**
(`aimy-ds.css`, `sales.css`, `bdr.css`, `bdr.js`) and **Knowledge** (`aimy-ds.css`,
`knowledge.css`, `knowledge.js`, `settings.css`).

The rewrite was **rule-aware, not regex-over-file**: each stylesheet is walked, every innermost
declaration block is matched against its own selector *and its ancestors*, and the change happens
inside the block or not at all. A regex cannot see a selector, and three surfaces were explicitly
out of scope.

- **415** font sizes, **634** ink references and **80** raw `rgba()` hues rewritten in the first pass.
- **69** shell rules adopted the reference implementation's size. The floor had been applied to
  `index.html` — which *is* the shell, inlined — and never propagated back to the copies each
  product ships, so `.pop-text` was 16px in the reference and 12px in both products. The doc and
  the code disagreed about a rule the doc already stated.
- **20** sizes in `rem`. Knowledge writes its own stylesheets against a fluid root
  (`html { font-size: max(1rem, calc(100vw / 96)) }`), so a px-shaped sweep walked straight past 9,
  10, 10.5, 11 and 13 pixels of type. Fixed **in rem** — converting to px would freeze those
  elements while everything around them still scales.
- **27** label-pill blocks lost their capitals, their tracking and their borders, across every
  pill in the system and not just `.tag`: `.work-state`, `.s-meta-st`, `.signal-badge`,
  `.trust-state`, `.conf-badge`, `.model-tag`, `.ver-tag`, `.entry-mode-tag`, `.tc-approval`,
  `.ws-track .ws-step`.
- **74** stale light-mode literals — the old saturated ramp, hard-coded inside
  `:root[data-theme="light"]` rules — replaced by the tokens, which already resolve to the light
  values in that context.
- In the products' JavaScript, a `tagCase()` helper at **16** render sites. It is at the render
  site on purpose: the same string is a tag on one screen and a button or a filter on another.

### The override is the last word, so it is the first place a floor has to reach

Everything above was applied to stylesheets and verified by reading them, and the products still
rendered body at 14px and meta at 13px. Reading a file is not the same as reading a screen.

**A product may re-declare a library token, and then the library's value never renders.** Three
places were doing it, none of them reached by a sweep over declarations:

- `Sales/sales.css` re-declares the whole `--fs-*` scale as 12 · 13 · 13 · 14 · 14, sitting after
  the shell in the cascade. The shell had been corrected to 12 · 14 · 16 and the product put it
  back.
- `Knowledge/knowledge.css` declares its own role scale, `--ty-*`, at 17 · 15 · 13 — three odd
  steps standing on a 12px floor.
- `Knowledge/knowledge.css` also keeps a **copy of the library's `--fs-*` scale in rem**, under a
  comment reading *"nothing here changes a value; every number is the library's own, divided by
  16."* That was true when the library's bottom step was 10px. It is 12px now, and the copy was
  still handing out 10 — so `.tc-approval` rendered at 10px through a shell that had already been
  corrected. A stale copy of a token is worse than no copy: it looks correct at both ends and is
  wrong in the middle.

Nineteen further sites in Knowledge wrote `0.875rem` as a literal where the token beside it held
the same value; those now read `var(--ty-meta)`, and its type-scale audit went from 21 findings to
3, all deliberate.

**And the shell was shipping unstamped.** `aimy-ds.css` was linked with no `?v=` in Sales's
`index.html` and both of Knowledge's pages, while every other asset carried one — so every shell
change since the stamps began has reached returning users only when their cache happened to expire.
Stamped, and all three products' stamps bumped together.

**The check that catches this is a runtime one.** Walk every rendered element, read its computed
`font-size`, exclude the carved-out surfaces by class, and assert that nothing is odd and nothing
is under 12. It found all three overrides in one pass, after the file-level sweep had reported
clean. The reference page, Sales and Knowledge now return 12 · 14 · 16 · 18 · 20 · 24 · 28 · 30 ·
32 · 34 · 40 · 46 · 54 and nothing else.

### What was deliberately left alone

**The top navigation, the chat input and the AiMY canvas.** Those three surfaces are shared chrome
with their own decisions, and **384 blocks** were carved out of the main sweep by selector. If a size or
an ink looks wrong there, it was skipped, not missed.

### Still open

- **QA runs the old pattern.** The screenshot that started this — saturated red and amber pills
  with matching borders, stacked in a column — is still live in QA, whose surfaces are standalone
  HTML files with inline styles rather than the shared shell. It is the same fix, in a different
  shape, and it has not been done.
- **`.form-summary`** carries a 3px `border-left` in `--err`. It is the one place a left-border
  stripe survives, and it should be a ground.
- **White on the unread badge is 3.76:1**, under the 4.5:1 small-text minimum. It has always been, on both the old `--err` and `--err-strong`; a filled alarm carrying two digits wants a darker ground or darker text, and that is a decision rather than a sweep.
- **Two orphaned rule bodies** in Sales's `sales.css` — declarations with no selector, leaving the
  file two braces short. Pre-existing, and unrelated to this sweep.
- **`.ds-select` vs `.v2-dropdown`** — resolved in favour of the custom dropdown; see §10.3.

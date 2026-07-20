# HTML Design System

Design rules to follow when building report HTML.

---

## When to Apply — **READ FIRST**

> Apply this design system **only when the user explicitly requests HTML report generation.** Never auto-apply it in any other case.

### ✅ Apply (user explicitly requests)

- "make it an HTML report"
- "in report format", "with this design system", "using the design system"
- "make a report/document HTML"
- "convert this PDF/material into a report"
- when continuing to write the same report from an earlier conversation

### ❌ Do not apply (no request, or a different task)

- **Simple Q&A** — "what is this?", "why does it work this way?", "how do I do it?"
- **Summaries/notes** — "organize this", "summarize this" (with no format specified)
- **Read-only** — "read this PDF", "tell me the contents", "check it"
- **Data/table only** — when a Markdown table, JSON, or code block is enough
- **Code review / debugging / design questions** — unrelated to this design system
- **Another format is specified** — PPT, DOCX, Markdown, single-page web, etc.

### Decision rules

1. Did the user explicitly mention one of "HTML", "report", "document", "NDS", or "this design"? → **If NO, do not apply.**
2. Even if related material is attached, if the request is "read it / tell me / summarize it", **do not apply.** Respond in Markdown/plain text.
3. If ambiguous, **ask**: "Should I make this an HTML report, or organize it as text?"

---

## 0. Principles

> **This is the Anthropic / Claude warm-editorial skin.** The look people recognize from "ask Claude to generate an HTML report": a warm ivory canvas (never pure white), warm brown-black ink (never cool gray), a single terracotta **clay** accent (never blue/slate), and serif display headlines over a humanist sans body.

1. **Warm, not clinical** — the canvas is ivory `#faf9f5`, not white; text is warm brown-black `#3D3929`, not cool `#191919`. Pure white and cool gray are banned. This warmth is the whole point of the skin.
2. **Editorial tone** — a literary-journal tone, not a marketing page. Minimize heavy shadows; favor ink + soft lines + gentle rounded corners (`--radius: 12px`).
3. **Typography first** — the type scale comes before components. Display headlines (cover title, PART H1, section H2) are **serif**; body/labels/numbers are Pretendard sans.
4. **One accent = clay** — the single emphasis color is terracotta clay `#D97757`. Limit color emphasis to 1–2 times per page; the default is the `--ink` family. Never introduce a second accent hue.
5. **Numbers must be crisp** — apply `font-feature-settings: "tnum"` to all numeric text.
6. **Don't fear whitespace** — `--section-py: 72px`, and 160px between the last section ↔ footer.

---

## 1. Color Tokens

> **Warm-only palette.** No pure white (`#ffffff`) as a page/text color, no cool gray. Every neutral carries a warm (brown/kraft) undertone. The only chromatic accent is clay.

### 1.1 Brand

```css
--brand-slate:      #141413;   /* warm near-black — dark surfaces (cover / PART) & headings */
--brand-ivory:      #faf9f5;   /* the signature canvas — page background */
--brand-clay:       #D97757;   /* THE accent — terracotta/coral (replaces the old blue) */
--brand-clay-deep:  #C96442;   /* deeper brick — hover / press / label text */
--brand-manila:     #EBDBBC;   /* warm sand — default callout tint */
--brand-kraft:      #D4A27F;   /* warm secondary tone */
--brand-red:        #BF4D43;   /* danger / confidential dot (warmed, not neon) */
--brand-green:      #617A5B;   /* positive trend (muted sage, not neon green) */
--brand-gray:       #B0AEA5;   /* warm mid gray */
```

### 1.2 Ink (warm brown-black text hierarchy)

```css
--ink:   #141413;   /* headings / body emphasis (slate) */
--ink-2: #3D3929;   /* default body — warm brown-black */
--ink-3: #605A4E;   /* secondary body / descriptions */
--ink-4: #83786A;   /* captions / labels */
--ink-5: #A8A093;   /* separators / disabled */
--ink-6: #C9C3B6;
```

### 1.3 Surface / Line (warm)

```css
--surface:    #faf9f5;   /* ivory page background (NOT #ffffff) */
--paper:      #ffffff;   /* card fill only — sits ON the ivory canvas for lift */
--surface-1:  #F2F0E9;   /* warm off-white */
--surface-2:  #EBE8DF;   /* thead / chart track (warm sand-gray) */

--line:        #141413;  /* strong divider (slate) */
--line-soft:   #E0DCD1;  /* warm hairline (card/table borders) */
--line-softer: #ECE9E0;  /* lightest warm separator (row dividers) */
```

> **`--surface` vs `--paper`**: the page is ivory (`--surface`); cards (KPI/problem/table cells) are pure `--paper` white so they lift gently off the warm canvas. This ivory-canvas + white-card contrast is a core Claude tell — do not paint the whole page white.

### 1.4 Semantic

```css
--accent:      #D97757;   /* = brand-clay  — the one accent */
--accent-deep: #C96442;   /* = brand-clay-deep — hover / label text */
--danger:      #BF4D43;   /* = brand-red   */
--success:     #617A5B;   /* = brand-green */
```

### 1.5 Radius (soft corners)

```css
--radius:    12px;   /* cards, tables, callouts, PART divider */
--radius-sm: 8px;
```

> Claude's warm cards use gentle rounded corners. Apply `--radius` to grouped components (`.kpi-row`, `.problem-grid`, `.table-wrap`, `.flow`, `.insight-list`, `.callout`, `.part-divider`) with `overflow:hidden` so inner 1px lines clip cleanly. Pills (`.badge`, chips) use `border-radius: 999px`.

---

## 2. Typography

### 2.1 Font family — sans body + serif display

> **Two families, split by role (the Claude type voice).** Body, labels, meta, numbers, and small headings (H3/H4) use **Pretendard** (humanist sans). **Display headlines — cover title, PART H1, section H2, and large KPI/insight numbers — use a warm serif** (Copernicus / Tiempos Headline → Korean 명조 fallback). This serif-display + sans-body pairing is the single strongest signal of the Claude look. Do not use other sans families (Inter, Noto Sans) for body, and do not set body copy in serif.

```css
--font-sans:    "Pretendard", sans-serif;
--font-mono:    "Pretendard", sans-serif;   /* mono slot is Pretendard — tnum keeps numbers aligned without swapping fonts */
--font-display: "Copernicus", "Tiempos Headline", "Noto Serif KR", Georgia, serif;   /* serif for headlines only */
```

CDN load:

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/static/pretendard.min.css" />
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Noto+Serif+KR:wght@500;600;700&display=swap">
```

#### Where serif applies (display only)

| Serif (`--font-display`) | Sans (`--font-sans`) |
| --- | --- |
| Cover title (`.cover-title`) | Everything else: body, lede, labels |
| PART header H1 (`.part-divider h1`) | H3 / H4 subheadings (sans keeps hierarchy contrast) |
| Section H2 (`.section-head h2`) | Table cells, TOC, footer, badges |
| Large numerals — `.kpi-value`, `.insight-num` | `.num-prefix`, mono meta, eyebrows (mono/sans) |

- **Korean support**: `"Noto Serif KR"` covers Korean 명조 glyphs; Latin falls to Copernicus/Tiempos (if present) then Georgia. Numbers in serif headings still get `font-feature-settings: "tnum"`.
- **Body stays Pretendard** — serif body copy hurts long-form Korean readability. Serif is reserved for large display sizes (20px+).

#### Weight usage

| Use | weight |
| --- | --- |
| Body (`<body>`) | 500 |
| Secondary body / labels | 500 ~ 600 |
| Mono / caption / label | 600 |
| Sans headings (H3/H4) / emphasis (strong) | 700 |
| **Serif display** (cover title / PART H1 / section H2 / KPI figures) | **600** (serif reads heavy at 700; 600 keeps it elegant) |

### 2.2 Type scale (~1.27× modular)

**Rule: the smallest font size is 12px. Nothing smaller.**

| Token | Size | Use |
| --- | --- | --- |
| `--fs-display-1` | **56px** | cover title / large KPI figures |
| `--fs-display-2` | **40px** | TOC section title |
| `--fs-h1` | **48px** | **PART (group) header** — top-level division grouping several sections |
| `--fs-h2` | **40px** | **section H2** — the heading that starts the body (bold) |
| `--fs-h3` | **20px** | section subheading / heading inside a card/component |
| `--fs-h4` | **15px** | secondary label heading (not used above tables — unify to H3) |
| `--fs-lede` | **17px** | section intro sentence (lede) |
| `--fs-body` | **15px** | body |
| `--fs-body-sm` | **13px** | secondary body / TOC items / footer title |
| `--fs-caption` | **12px** | caption |
| `--fs-micro` | **12px** | labels / mono meta |
| `--fs-micro-xs` | **12px** | minimum size (nothing under 12px) |

#### Heading hierarchy — line & margin rules (important)

> **Only H1 & H2 have a divider. H3 & H4 never have a line.**
> **Margins shrink with hierarchy: H1 (largest) > H2 > H3 > H4 (smallest).** Even H4 keeps enough margin to be clearly separated from the body.

| Heading | Size | Line | margin-top |
| --- | --- | --- | --- |
| **H1 (PART header)** | **48px** / **serif** / weight 600 | **6px solid top** (thickest) | **120px** (largest) — new chapter-level division |
| **H2 (section)** | **40px** / **serif** / weight 600 | **3px solid top** (`.section-tag` or equivalent) | section padding 72px |
| **H3 (subheading)** | 20px / sans / weight 700 | **no line** | 56px |
| **H4 (small label)** | 15px / sans / weight 700 | **no line** | 36px |

> **H1 & H2 are serif (`--font-display`, weight 600); H3 & H4 stay sans (Pretendard, weight 700).** The serif/sans switch at the H2→H3 boundary is intentional — it reinforces the hierarchy and carries the Claude editorial voice.

If a heading above a table was an H3, its line is automatically removed (design system rule). If it was a component that used to have a line (`.block-head`, etc.), remove the line.

### 2.3 Line-height tokens

```css
--lh-tight:  1.15;   /* display */
--lh-snug:   1.25;   /* headings */
--lh-normal: 1.4;
--lh-loose:  1.7;    /* body / lede */
```

### 2.4 Letter-spacing — a conservative policy tuned for Korean

> **Body-area headings (H2–H4), subheadings, number prefixes, and small labels are all unified to letter-spacing 0.** Adjusting Korean text with negative/positive letter-spacing actually hurts readability. The design convention of giving positive letter-spacing (spacing) to English mono uppercase labels also looks awkwardly stretched when Korean appears alongside.
>
> Keep positive letter-spacing only for intentional English areas like the **cover/footer chip/eyebrow**.

| Area | letter-spacing |
| --- | --- |
| Display 1 (cover title, 56px, **serif**) | `-0.02em` (serif needs less negative tracking than sans) |
| Display 2 (large display, 40px) | `-0.02em` |
| H1 (PART header, 48px, **serif**) | `-0.01em` |
| H2 (section, 40px, **serif**) | **`-0.01em`** |
| H3 / H4 (subheading · table label, sans) | **`0`** |
| `.num-prefix` (section number) | **`0`** |
| Body labels (`.kpi-label`, `.metric-label`, `.block-head .meta`, `.ph-label`, `.step-num`, `.bar-legend`, etc.) | **`0`** |
| lede / body | `-0.005em` (Korean adjustment) |
| **Cover/footer English chip/eyebrow** (`.cover-eyebrow`, `.cover-confidential`, `.cover-meta-label`, `.footer-confidential`) | `+0.14~0.18em` (editorial asset context, preserved) |

#### Application principles

- No letter-spacing on body headings and labels — keeps the tone of a Korean report.
- Restrict positive letter-spacing to roughly the "English meta chip of cover/footer" only. Do not indiscriminately give positive letter-spacing to body mono labels.
- Use negative letter-spacing only on large display text (36px+). **Serif display** takes lighter tracking (`-0.01em` ~ `-0.02em`) than the old sans display did (`-0.04em`) — serifs already sit tighter, so heavy negative tracking crowds them.

### 2.5 Body (`<body>`) defaults

```css
font-family: var(--font-sans);
font-size:   var(--fs-body);     /* 15px */
line-height: var(--lh-loose);    /* 1.7  */
font-weight: 500;
color:       var(--ink-2);
font-feature-settings: "ss01", "cv11", "tnum";
```

---

## 3. Korean Writing Rules

### 3.1 Word-level line breaking (required)

Prevents Korean from being awkwardly broken mid-word at the syllable level.

```css
body {
  word-break: keep-all;
  overflow-wrap: break-word;
}
```

### 3.2 Heading style

- Unify headings to noun form (e.g., "Revenue Structure", "Market Opportunity"). Do not use interrogative headings ("...?").

> Prose style (sentence endings, tone) varies by department and document type, so the design system does not prescribe it. Leave it to the author's discretion.

### 3.3 Lede — section intro (system rule)

The intro sentence right below the section header. Length is 1–2 paragraphs; width follows the body (`--max`). Content and style are at the author's discretion.

> **No triple duplication of one-line summary + body + callout** (component usage rule). Putting a body paragraph with the same content right below a short lede is repetitive. Unify the intro as a lede (1–2 paragraphs), and add a callout only when there is a separate takeaway (see Section 8).

```css
.lede {
  font-size: var(--fs-lede);
  line-height: var(--lh-loose);
  letter-spacing: -0.005em;
  color: var(--ink-3);
  font-weight: 500;
}
.lede + .lede { margin-top: 16px; }   /* paragraph gap for a 2-paragraph intro */
.lede b { color: var(--ink); font-weight: 700; }   /* emphasize key phrases */
```

### 3.4 Mixing numbers / English / Korean

- Latin glyphs from Pretendard are used automatically for English and numbers. No extra handling needed.
- Where alignment matters, such as tables/KPIs: `font-feature-settings: "tnum"` or `class="tnum"`.

---

## 4. Layout Tokens

```css
--max:        800px;    /* body area max-width (shared by cover/section/footer) */
--narrow:      760px;   /* narrow body (long-form text sections) */
--pad-x:        56px;   /* left/right padding (mobile 24px) */
--section-py:   72px;   /* section top/bottom padding (mobile 64px) */
```

- **Every area aligns to `--max`** (cover, body, TOC sections, footer). This is the basis of readability and alignment consistency.
- Gap between body ↔ side navigation: **40px** (constant at 1500px and above).
- Last section ↔ footer: `margin-top: 160px` (mobile 96px).

---

## 5. Cover Structure

Slate full-bleed + 60vh min-height + `--max` alignment. The dark cover band is warm slate `#141413` (not cool black) lit by a clay glow — a warm inversion of the ivory page.

```html
<section class="cover" id="cover">
  <div class="cover-inner">
    <div class="cover-head">
      <div class="cover-head-main">
        <div class="cover-eyebrow">Payment &amp; Coupon Market Analysis</div>
        <h1 class="cover-title">Payment &amp; Coupon Market Analysis</h1>
        <p class="cover-summary">
          A comparative analysis of the pay-payment environment across four markets — Korea, US, China, Japan — from a transaction-volume and revenue-structure perspective.<br>
          Baseline material for establishing a mid-to-long-term strategy for the payments business.
        </p>
      </div>
      <span class="cover-confidential">CONFIDENTIAL</span>
    </div>
    <div class="cover-meta">
      <div class="cover-meta-item"><span class="cover-meta-label">Date</span>   <span class="cover-meta-value mono">-</span></div>
      <div class="cover-meta-item"><span class="cover-meta-label">Team</span>   <span class="cover-meta-value">-</span></div>
      <div class="cover-meta-item"><span class="cover-meta-label">Author</span> <span class="cover-meta-value">-</span></div>
    </div>
  </div>
</section>
```

### 5.1 Structural rules

- Background — `--brand-slate` (#141413) base beneath a **subtle clay radial glow**. Text is `--brand-ivory` (#faf9f5).

  ```css
  .cover {
    background:
      radial-gradient(ellipse 70% 55% at 22% 0%, rgba(217, 119, 87, 0.28), transparent 62%),   /* top-left clay spotlight */
      radial-gradient(ellipse 60% 50% at 92% 100%, rgba(212, 162, 127, 0.14), transparent 60%), /* bottom-right kraft spotlight (weaker) */
      var(--brand-slate);
    overflow: hidden;
  }
  ```

  - Subtle warmth + depth. At normal viewing it reads as warm near-black; up close there's a top-left clay 28% / bottom-right kraft 14% glow. Both accents are warm — no cool blue on the cover.
  - No impact on content readability (the background tone over the text stays near black).
- `padding: 96px var(--pad-x)`, `min-height: 60vh`.
- Even spacing between the top and bottom areas (`cover-head` ↔ `cover-meta`) via `flex justify-content: space-between`.
- **eyebrow**: English, mono, micro size, `letter-spacing: 0.16em`, uppercase.
- **title**: **serif** (`--font-display`), `--fs-display-1` (56px), **line-height 1.2**, weight **600** (serif reads heavy at 700). `letter-spacing: -0.02em`. Korean title. This serif title is the cover's defining Claude cue.
- **summary**: `--fs-lede` (17px), ivory 74% alpha, concise 2–3 lines (`<br>` once or twice). **This is a cover-only subtitle, distinct from a section lede (1–2 paragraphs)** — do not write it long on the cover.
- **confidential**: top-right **pill** chip (`border-radius: 999px`) — clay dot + uppercase mono. Visually identical to the body footer chip.
- **meta**: **3-column grid** — `Date / Team / Author`. Labels are English uppercase mono; values are Korean/numbers.
- Grid CSS: `grid-template-columns: repeat(3, auto)`.

### 5.2 Meta value input rules

> **The three meta values (Date · Team · Author) are entered by the user (author) for each report.** There is no default hardcoded in the system; when empty, display **`-`** (en-dash or hyphen).

| Field | Format | Example | If empty |
| --- | --- | --- | --- |
| `Date` | **`YYYY.MM.DD`** (mono) | `2025.05.04` | `-` |
| `Team` | Korean department/part name | `UX Part` | `-` |
| `Author` | Korean name | `Hong Gil-dong` | `-` |

#### Date format rule — unify to `YYYY.MM.DD`
>
> **All date notation on the cover/footer is unified to `YYYY.MM.DD` (dot separators, 4-digit year).** Do not use other formats (`YY/MM/DD`, `YYYY-MM-DD`, `YYYY년 M월 D일`, etc.).

| Item | Correct | Wrong |
| --- | --- | --- |
| 4-digit year | `2025.05.04` | `25.05.04` (century ambiguous) |
| Separator | dot (`.`) | `-`, `/`, `year month day` |
| Zero padding | `2025.05.04` | `2025.5.4` |
| Font | mono (`tnum`) — apply `class="mono"` | regular body |

Reasons:

- 4-digit year removes century ambiguity.
- The dot separator is the Korean publishing/official-document convention. Clean with a mono font.
- Zero padding maintains monospaced alignment (consistent across reports and filenames).
- Short and identifiable even in the footer's short single-line meta.

#### Other rules

- **Do not use a Version field.** Version control is handled by git/filename; it is not shown in the cover meta.
- Do not use a "Department" label either (unify to Team).

---

## 6. Side Navigation (Side Nav / TOC)

> **Do not use a fixed top bar (top nav).** A report is a single document, and a sticky bar that permanently occupies the top of the page obscures content and gets in the way when printing. In-document movement is handled solely by the **side nav**.

Borrows the Claude Support rail pattern. Always floating on the **left** of the body, highlighting the active section.

### 6.1 Markup — H1 (PART) + H2 (section) hierarchy

> **The side nav exposes only two hierarchies: H1 (PART group) and H2 (section).** It does not expose H3 or below (flattening to depth 1 explodes the length). Reports without PARTs list only H2.

```html
<aside class="side-nav" aria-label="Section navigation">
  <ul class="side-nav-list">
    <!-- H1: PART group header — stronger visual hierarchy -->
    <li><a href="#part-1" data-target="part-1" class="sn-h1">
      <span class="sn-num">PART I</span><span class="sn-title">Global Market</span>
    </a></li>

    <!-- H2: sections within that PART (indented + smaller text) -->
    <li><a href="#exec"     data-target="exec"><span class="sn-num">01</span><span class="sn-title">Key Metrics</span></a></li>
    <li><a href="#overview" data-target="overview"><span class="sn-num">02</span><span class="sn-title">Market Overview</span></a></li>
    <!-- ... -->

    <li><a href="#part-2" data-target="part-2" class="sn-h1">
      <span class="sn-num">PART II</span><span class="sn-title">Domestic Market</span>
    </a></li>
    <!-- sections of the next PART ... -->
  </ul>
</aside>
```

### 6.2 Style essentials

```css
.side-nav {
  position: fixed;
  top: 96px;
  /* body left edge − 40px − nav width (200px). But if the screen is narrow, keep 24px from the viewport left */
  left: max(
    24px,
    calc(50% - (var(--max) / 2) - 40px - 200px)
  );
  z-index: 90;
  width: 200px;
  max-height: calc(100vh - 128px);
  overflow-y: auto;
}
.side-nav-list { border-left: 2px solid var(--line-soft); }
.side-nav-list a {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 8px;
  align-items: baseline;
  padding: 7px 0 7px 12px;
  margin-left: -2px;
  border-left: 2px solid transparent;
  color: var(--ink-4);
}
.side-nav-list a:hover { color: var(--ink); }
/* Active = clay accent (left bar, title, and num all unified to one emphasis color) */
.side-nav-list a.active { color: var(--accent); border-left-color: var(--accent); }
.side-nav-list a.active .sn-num { color: var(--accent); }
.side-nav-list a.active .sn-title { color: var(--accent); }

/* H1 & H2 shared — stacked on the same vertical rail. Both use the same padding/rhythm, same active left bar, same left edge.
   No indent — the only difference is typography (H1: weight 700 · uppercase eyebrow, H2: weight 500 · body-sm). */
.side-nav-list .sn-num   { font-family: var(--font-mono); font-size: var(--fs-micro); font-weight: 600; color: var(--ink-5); letter-spacing: 0; }
.side-nav-list .sn-title { font-size: var(--fs-body-sm); font-weight: 500; line-height: var(--lh-snug); letter-spacing: -0.005em; color: var(--ink-4); }

/* H1 entries (PART group header) — same gray tone as H2. Only the typography is prominent (weight 700 · uppercase eyebrow). */
.side-nav-list a.sn-h1 { color: var(--ink-4); }
.side-nav-list a.sn-h1 .sn-num   { font-size: 11px; letter-spacing: 0; font-weight: 700; color: var(--ink-4); text-transform: uppercase; }
.side-nav-list a.sn-h1 .sn-title { font-size: 13px; font-weight: 700; color: var(--ink-4); }

/* ⚠ Specificity pitfall — a separate H1 active rule is required.
   `.side-nav-list a.active .sn-num` (0,3,1) and `.side-nav-list a.sn-h1 .sn-num` (0,3,1) have the same specificity, and
   since the H1 default comes later in source it overrides the active rule. → Use `.sn-h1.active` to gain specificity (0,4,1). */
.side-nav-list a.sn-h1.active,
.side-nav-list a.sn-h1.active .sn-num,
.side-nav-list a.sn-h1.active .sn-title { color: var(--accent); }

/* H2 indent — applied only in a nav that has PARTs (.sn-h1). Expresses that H2 is subordinate under H1 via indent.
   Not applied to reports without PARTs (flat H2 list) — scoped with :has(). */
.side-nav-list:has(a.sn-h1) a:not(.sn-h1) { padding-left: 20px; }

@media (max-width: 1499px) { .side-nav { display: none; } }
```

### 6.3 Responsive behavior rules

| Viewport | Body left ↔ TOC right gap |
|---|---|
| ≤ 1499px | Hide TOC |
| ≥ 1500px | **Fixed 40px** (aligned to the body) |

> Core principle: pin the TOC not at the viewport's left but at **body left edge − 40px**. With `max(24px, …)`, put a lower bound so the left doesn't go negative and off-viewport on small screens.
> With an 800px body, at the display start point (1500px) there is already `50% − 400 − 40 − 200 = 110px` of room, so the lower bound (24px) is never triggered in the visible range — the lower bound acts only as a safety net with no separate transition range.

### 6.4 Initial position + active tracking (JS)

```javascript
document.addEventListener('DOMContentLoaded', function() {
  const nav     = document.querySelector('.side-nav');
  const links   = document.querySelectorAll('.side-nav-list a');
  const map     = {};
  links.forEach(a => { map[a.dataset.target] = a; });
  const sections = Object.keys(map).map(id => document.getElementById(id)).filter(Boolean);
  /* Anchor decision:
     - If the first navigated section is a PART (.part-divider), use the top of the .part-divider card fill as the anchor.
     - For a normal section, use its inner h2 (or h1) as the anchor.
     A PART has a card fill, so aligning to the card top (= section box top) looks natural,
     while a normal section is more natural aligned to its content start (h2) above the padding. */
  const firstSection = sections[0];
  const isPartFirst  = firstSection && firstSection.classList.contains('part-divider');
  const anchorEl     = isPartFirst ? firstSection : (firstSection?.querySelector('h1, h2') || firstSection);
  const PIN_TOP  = 32;

  function getAnchorY() { return anchorEl.getBoundingClientRect().top + window.scrollY; }
  function update() {
    const y = window.scrollY + window.innerHeight * 0.3;
    let active = sections[0];
    for (const s of sections) { if (s.offsetTop <= y) active = s; }
    links.forEach(a => a.classList.remove('active'));
    if (active && map[active.id]) map[active.id].classList.add('active');
    if (nav && anchorEl) {
      const anchorY = getAnchorY();
      nav.style.top = Math.max(PIN_TOP, anchorY - window.scrollY) + 'px';
    }
  }
  window.addEventListener('scroll', update, { passive: true });
  window.addEventListener('resize', update);
  update();
  /* Recompute after fonts/images load — prevents the initial anchorY from being off due to layout changes (required) */
  if (document.fonts && document.fonts.ready) document.fonts.ready.then(update);
  window.addEventListener('load', update);
});
```

- The TOC starts at the first section's box top (for a PART) or the first H2's top (for a normal section) → once you scroll, it pins 32px from the top.
- **`document.fonts.ready` + `window.load` recompute is required** — before Pretendard loads, heading height/position are computed against the fallback font, throwing off the anchor. After the font loads you must run update once more to align at the exact position.
- The `.active` class = the section that most recently passed the 30% body line (PARTs included).

### 6.5 Item notation rules

- **Number (`sn-num`) + Korean title (`sn-title`)**, gap 8px (narrow enough to read as attached).
- Titles are static noun form (`Revenue Structure`, `Market Opportunity`). No interrogatives.
- **H2 section numbers** are always two digits (`01`, `02`, …). Appendix is `APX`.
- **H1 PART numbers** are Roman numerals (`PART I`, `PART II`, …).
- Add `class="sn-h1"` to H1 items and keep the same markup structure as H2 (`.sn-num` + `.sn-title`).

### 6.6 Scroll-to-Top floating button (`.scroll-top`)

> **Every report has a bottom-right floating "back to top" button.** This reduces the burden of scrolling far up to click the side nav in a long report. It must also work on narrow screens (<1500px) where the side nav is hidden.

#### Markup

```html
<button class="scroll-top" type="button" aria-label="Back to top">
  <svg width="14" height="14" viewBox="0 0 14 14" fill="none" aria-hidden="true">
    <path d="M7 11V3M7 3L3 7M7 3L11 7" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
  </svg>
</button>
```

#### Style

```css
.scroll-top {
  position: fixed;
  right: 32px;
  bottom: 32px;
  width: 44px;
  height: 44px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  background: var(--accent);
  color: var(--brand-ivory);
  border: none;
  border-radius: 999px;
  cursor: pointer;
  opacity: 0;
  pointer-events: none;
  transform: translateY(8px);
  transition: opacity var(--dur) var(--ease),
              transform var(--dur) var(--ease),
              background var(--dur) var(--ease);
  box-shadow: 0 6px 20px rgba(20, 20, 19, 0.18),
              0 1px 2px rgba(20, 20, 19, 0.08);
  z-index: 100;
}
.scroll-top.visible {
  opacity: 1;
  pointer-events: auto;
  transform: translateY(0);
}
.scroll-top:hover  { background: var(--accent-deep); }
.scroll-top:active { transform: translateY(0) scale(0.96); }
.scroll-top:focus-visible {
  outline: 2px solid var(--accent);
  outline-offset: 2px;
}
@media (max-width: 880px) {
  .scroll-top { right: 20px; bottom: 20px; }
}
```

#### JS — visibility & behavior

```javascript
document.addEventListener('DOMContentLoaded', function() {
  const btn = document.querySelector('.scroll-top');
  if (!btn) return;
  /* Show after scrolling one viewport or more. Appearing too soon is visual noise */
  const SHOW_AFTER = Math.max(600, window.innerHeight * 0.6);
  function toggle() {
    btn.classList.toggle('visible', window.scrollY > SHOW_AFTER);
  }
  btn.addEventListener('click', () => {
    window.scrollTo({ top: 0, behavior: 'smooth' });
  });
  window.addEventListener('scroll', toggle, { passive: true });
  window.addEventListener('resize', toggle);
  toggle();
});
```

#### Rules

- **Position**: fixed bottom-right of the viewport. `right: 32px; bottom: 32px` (mobile 20px).
- **Size**: 44×44px (minimum touch target). `border-radius: 8px` (rounded square).
- **Color**: background `var(--accent)` (clay), ivory icon — the pill-shaped primary floating action, matching Claude's clay CTA. `border-radius: 999px`. (One-accent system: the same clay as the side-nav active state; the button is set apart by its filled pill shape and shadow, not by hue.)
- **Icon**: up-arrow SVG (`↑`). Size 14×14px, 1.5px stroke. Do not use emoji/unicode arrows (rendering consistency).
- **Show condition**: `scrollY > 600px` or `0.6 × innerHeight` (whichever is larger). Hidden on the first screen.
- **Disappear**: auto-hide when reaching the top. Smooth via transition.
- **shadow**: `0 6px 20px rgba(25,25,25,0.18)` — an impression of floating above the body. An **exception** to NDS's general shadow-restraint principle (floating UI requires shadow).
- **z-index separated from the side nav**: side-nav `z-index: 90`, scroll-top `z-index: 100` — the button is always on top even if the two overlap.
- **a11y**: `aria-label="Back to top"` required; show an `outline` on keyboard focus (focus-visible).
- **Click behavior**: smooth scroll via `window.scrollTo({ top: 0, behavior: 'smooth' })`. Also recommend enabling `html { scroll-behavior: smooth }` (see 11. Motion).

---

## 7. Section

```html
<section class="section [muted]" id="...">
  <div class="section-inner">

    <!-- 7.1 section line — line only, no text -->
    <div class="section-tag"></div>

    <!-- 7.2 section head — simple H2 + lede structure -->
    <div class="section-head">
      <h2><span class="num-prefix">01</span>Revenue Structure</h2>
      <p class="lede">…(section intro, 1–2 paragraphs)…</p>
    </div>

    <!-- 7.3 body subheading + component — wrap the title and table together with .block -->
    <div class="block">
      <div class="block-head"><h3>Subheading</h3></div>
      <div class="table-wrap">…</div>
    </div>

    <!-- 7.4 section closing callout -->
    <div class="callout">…</div>

  </div>
</section>
```

> **Layout structure: `--max` alignment is handled by `.section-inner`.** `main` (or `.section`) holds the left/right `--pad-x` padding, and the inner `.section-inner` sets the body width with `max-width: var(--max); margin: 0 auto`. This is the same structure as the cover (`.cover-inner`) and footer (`.footer-inner`), so all four areas' left/right edges align on one vertical line. Do not put `max-width` directly on `main` and add padding on top of it — that narrows the body to `--max − 2×pad-x` and misaligns it from the cover/footer, so it's forbidden.

```css
main { padding: 0 var(--pad-x); }
.section { padding: var(--section-py) 0; }
.section-inner { max-width: var(--max); margin: 0 auto; }
```

### 7.1 Section line (`section-tag`)

> **`section-tag` draws exactly one line.** It shows none of its inner elements (children hidden for legacy markup compatibility). No English meta.

```css
.section-tag { border-top: 3px solid var(--line); margin-bottom: 28px; min-height: 0; }
.section-tag > * { display: none !important; }
```

### 7.2 Section head — simple H2 + lede structure

> **The section head consists only of H2 (number + Korean title) + lede (intro sentence).** Do not put an English meta label to the right of the title — it splits attention and weakens the tone of the Korean body.

```html
<div class="section-head">
  <h2><span class="num-prefix">01</span>Revenue Structure</h2>
  <p class="lede">…(section intro, 1–2 paragraphs)…</p>
</div>
```

```css
.section-head { display: block; margin-bottom: 56px; }
.section-head > h1, .section-head > h2 { margin-bottom: 24px; }

/* Force H2 to always be the serif token size (40px) — override other classes like display-xl (!important) */
.section-head h2,
.section-head h2.display-xl,
.section-head h2.display-xxl {
  font-family: var(--font-display) !important;   /* serif headline */
  font-size: var(--fs-h2) !important;     /* 40px */
  line-height: var(--lh-snug) !important;
  letter-spacing: -0.01em !important;
  font-weight: 600 !important;            /* serif reads heavy at 700 */
  color: var(--ink) !important;
}

/* Number prefix — mono + clay accent, sits inline before the serif title */
.section-head h2 .num-prefix {
  font-family: var(--font-mono);
  display: inline-block;
  margin-right: 16px;
  color: var(--accent);
  font-weight: 600;
}
```

#### Head authoring rules

- In `<h2>`, place `.num-prefix` (section number) + Korean title. Numbers are two digits (`01`, `02`, …); appendix is `APX`.
- **Every section H2 is forced to the same serif 40px / weight 600.** Even combined with another display class (`display-xl`, etc.), specify `!important` in CSS so serif 40px is automatically applied.
- **`.num-prefix` is mono + clay accent** — the section number is the one small spot of accent color in the head, set just before the serif title.
- Titles are **static noun form**. No interrogatives ("...?").
- The `<p class="lede">` intro is **1–2 paragraphs** (see 3.3). Don't cut it to a short single line, and don't duplicate it with a separate body paragraph.
- ❌ **Do not use an English meta label to the right of the title.**

### 7.3 Body subheading — choose one of 2 patterns

Body subheadings use **one of two patterns to fit the situation**. The deciding factor is whether to place H3 alone or tie H3 + right-side meta on one line.

> **A title above a table is always H3 (Pattern A).** Regardless of size, a title above a data component (table/chart/KPI, etc.) is not demoted to H4. Even with several tables in a row, unify them all as H3 — hierarchy consistency takes priority over readability.

#### A. **Section-direct H3 (20px, no line)** — when the component has its own top line (default)

Most NDS components — tables (`.table-wrap`), KPI rows (`.kpi-row`), distribution lists, etc. — have their own `border-top`. Giving H3 an underline here causes a **double-line problem**. → Separate H3 **with margin only**.

> **❗ Wrap the title and component together with `.block`.** Placing H3 and the table as direct siblings of `.section-inner` makes the table inherit the section rhythm (`.section-inner > * { margin-top: 56px }`), so the **gap between the title and table becomes 56px** — the same as the gap between unrelated blocks, making the title look separated from its own table. Putting the title+component inside one `.block` makes both take the block rhythm (`.block > * + * { margin-top: 24px }`), so the **table attaches to the title at 24px**, and 56px applies only at the outer edges of `.block`. That is, 56px (between blocks) and 24px (within a block) each operate in their proper place.

```html
<div class="block">
  <div class="block-head"><h3>Quarterly Transaction Volume (2024)</h3></div>
  <div class="table-wrap"><table>…</table></div>
</div>
```

```css
h3, .h3 { font-size: var(--fs-h3); line-height: var(--lh-snug); letter-spacing: 0; font-weight: 700; color: var(--ink); }   /* --fs-h3 = 20px, weight 700 — same value as .section-inner h3 below */

/* All h3 within a section (descendant) — 56px top margin at any depth.
   margin-bottom is 0 — the next element's own margin determines the gap (avoids double-adding). */
/* Inherit the base h3 (20px/700) as-is — here we only add section rhythm (margin) */
.section-inner h3 {
  margin-top: 56px;
  margin-bottom: 0;
}
.section-inner h3:first-child { margin-top: 0; }

/* h3 inside a card component — the card's own layout handles it, top margin 0 */
.problem-card h3, .brand-card h3, .phase h3 { margin-top: 0; }

/* .block — title+component pairing. Outer is 56px section rhythm, inner is 24px block rhythm */
.block > * + * { margin-top: 24px; }
.block > .callout { margin-top: 32px; }
```

> **Why margin-bottom is 0** — if you give a heading a bottom margin, it overlaps (or adds to) the next element's top margin, making visual gaps uneven. Use a one-directional rule where headings give only a top gap and body elements give only their own top gap — then gaps stay consistent in any combination.

> **Why a descendant selector (`.section-inner h3`)** — this guarantees a consistent 56px top margin even when the h3 sits at various depths (inside `.block`, or inside `.g2 > .block > .block-head`, etc.). Using only `.section-inner > h3` (direct child) applies to direct h3 only, dropping margins on h3 at other depths.

#### B. **`.block-head` wrapper (20px, no line)** — when you want H3 + right-side meta on one line

`.block-head` is merely a **layout wrapper** that ties H3 and right-side meta (unit, note, etc.) onto one row. It **draws no line of its own** (heading rule: H3 has no line).

```css
.block { margin-top: 56px; }
.block:first-child { margin-top: 0; }
.block-head {
  margin-bottom: 20px;
  padding-bottom: 0;            /* no line */
  border-bottom: none;          /* ❗ never add a line */
  display: flex;
  justify-content: flex-start;  /* meta sits inline right next to h3 */
  align-items: baseline;
  gap: 12px;
  flex-wrap: wrap;
}
.block-head h3 {
  font-size: 20px;
  font-weight: 700;
  line-height: var(--lh-snug);
  letter-spacing: 0;
  color: var(--ink);
}
.block-head .meta {
  font-family: var(--font-mono);
  font-size: var(--fs-micro);
  color: var(--ink-4);
  letter-spacing: 0;
  text-transform: uppercase;
}
```

#### Pattern selection criteria (summary table)

| Situation | Pattern | Heading hierarchy |
| --- | --- | --- |
| Subheading within a section / title above a table/chart (standalone H3) | **A: `<h3>`** (20px, no line) | Strong |
| When you want H3 + right-side meta (unit, period, etc.) on one line | **B: `.block-head h3`** (20px, no line) | Strong |

#### Common rules

- **H3 never has a line.** (See the heading hierarchy rule in the token table above.)
- **A subheading must be visually stronger than body data values.**
- **A title above a data component (table/chart/KPI, etc.) is always H3.** Do not demote to H4. Even with several tables in a row within one section, unify them all as H3.
- Do not use H4 (15px) as a body subheading — unify table/component titles to H3.

### 7.4 Section vertical rhythm — the `.section-inner > *` rule

> **Every top-level child in a section gets a consistent 56px top margin.** Don't hardcode margin-top on the components; the parent container manages it uniformly — controlling rhythm in one place is the key to preventing unevenness.

```css
/* Level 1: direct children of section — consistent 56px gap */
.section-inner > * { margin-top: 56px; }
.section-inner > *:first-child { margin-top: 0; }
.section-inner > .section-tag,
.section-inner > .section-head { margin-top: 0; }   /* the section's own start — no extra margin */

/* Level 2: inside a grid, child margins duplicate the grid gap. Always use grid gap only */
.g2 > *, .g3 > * { margin-top: 0 !important; }

/* Level 3: inside .block — uniform 24px rhythm (callout only 32px).
   ❌ Do not add a rule like `.block { margin-top: 0 }` — it has the same specificity as the Level 1 rule and, coming later in source, overrides Level 1 (see the pitfall below). */
.block > * + * { margin-top: 24px; }
.block > .callout { margin-top: 32px; }

/* .callout: breathes only on top; the bottom is handled by the next sibling's margin-top (avoids double counting) */
.callout { margin-top: 32px; margin-bottom: 0; }
```

#### Specificity caution — don't hardcode margins on components

`.section-inner > *` (specificity 0,1,0) is the same grade as `.block { margin:0 }` (0,1,0), so redeclaring `margin` on a component class conflicts by source order and nullifies the 56px/24px rhythm (headings stick to the content above).

- **Do not redeclare `margin:0` on component classes.** The global `*{margin:0}` reset already handles it, so components specify a positive margin only when needed. (e.g., `.bul{list-style:none;padding:0;}` — omit `margin:0`)
- Container rhythm is owned entirely by `.section-inner > *` (level 1), `.g2/.g3 > *` (level 2), and `.block > * + *` (level 3). If you need higher priority, specify with two classes like `.section-inner > .block` (0,2,0).
- Intent: if each component gets its own margin, combinations merge or collapse and make gaps uneven. Rhythm must be controlled in one place to stay consistent.

#### Margin scale summary

| Location | Gap |
| --- | --- |
| Between direct children of a section (`.section-inner > * + *`) | **56px** |
| Between grid (`.g2`, `.g3`) children | grid `gap: 56px` |
| Between children inside a block (`.block`) | **24px** |
| Above a callout in a block (`.block > .callout`) | **32px** |
| Above a heading (h1/h2/h3/h4) | by hierarchy (see the 2.2 heading hierarchy table) |

### 7.5 Section-internal layout — prefer top/bottom placement

> **Placing two data blocks (table/chart/list) side by side is forbidden by default.** When Korean body + a table overlap, the horizontal width narrows, text breaks, tables wrap, and readability collapses. Make **stacking vertically (top/bottom) the default.**

```css
/* g2: two children vertically (NDS default) */
.g2 { display: grid; grid-template-columns: 1fr; gap: 56px; }

/* g3: for comparing 3 short stats (horizontal OK) */
.g3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; }
```

#### When to use horizontal placement

Allow horizontal comparison only when **all** of the following hold.

- The child blocks **contain no tables**.
- Each block's body text is short (within 2–3 lines).
- An explicit **left/right comparison** like "A vs B" is meaningful.

Otherwise, place everything vertically (`.g2`).

### 7.6 Table — header/cell alignment consistency

```css
/* Warm rounded card: a full 1px soft border with --radius, clipped by overflow:hidden */
.table-wrap { border: 1px solid var(--line-soft); border-radius: var(--radius); overflow: hidden; }
.table-wrap.scroll { overflow-x: auto; }   /* add .scroll when the table can exceed --max */
table { width: 100%; border-collapse: collapse; font-size: 13px; }
/* thead background is warm sand-gray (--surface-2 = #EBE8DF) + slate text. A warm light tone that doesn't break the ivory body flow */
thead th { text-align: left; padding: 12px 16px; background: var(--surface-2); color: var(--ink); font-family: var(--font-mono); font-size: var(--fs-micro); text-transform: uppercase; letter-spacing: 0; font-weight: 600; white-space: nowrap; }
thead th.num, td.num { text-align: right; font-feature-settings: "tnum"; }
tbody td { padding: 14px 16px; border-bottom: 1px solid var(--line-softer); color: var(--ink-2); vertical-align: top; font-size: 13.5px; }
tbody tr:last-child td { border-bottom: none; }
```

#### thead background color rule

- Background is **`--surface-2` (#EBE8DF)** — warm sand-gray. Do not use slate (`--ink`) or cool gray.
- A dark header carries too much visual weight and breaks the body flow when there are several tables on a page. A warm light gray keeps header identifiability while blending into the ivory canvas.
- Use dark text (`var(--ink)`) — ink contrast over `--surface-2` stays well above WCAG AA.

#### Rounded warm cards

- Grouped components (`.table-wrap`, `.kpi-row`, `.problem-grid`, `.flow`, `.insight-list`) use a **full 1px `--line-soft` border + `--radius` (12px) + `overflow:hidden`**, instead of the old top/bottom-only black rule. The soft warm border + gentle radius is the Claude card look. Inner separators stay 1px.
- Card fills are **`--paper` (#fff)** so they lift off the ivory page; the page itself is never white.

#### Alignment rules

- **Attach `class="num"` to every numeric column on both the header (`<th>`) and all cells (`<td>`), without omission.** If one side is missing, header and cell alignment goes out of sync.
- On numeric cells, enable monospaced numbers with `class="num tnum"` (or `font-feature-settings: "tnum"`).
- Unify `vertical-align: top` on all `tbody td`. Do not use middle (it throws off hierarchy in multi-line cells).
- Always wrap tables in `.table-wrap`. If the table width can exceed the content area (`--max`), enable horizontal scroll with `overflow-x: auto`.
- Do not force cell content to wrap.

#### Line thickness rule — all table lines 1px MAX

> **All outlines of tables (`.table-wrap`, `.steps`, `.flow`, `.breakdown-list`, `.geo-grid`, and other table/list-type components) are 1px maximum.** Thick lines of 2px+ carry too much visual weight, break the body flow, and create visual clutter when several tables appear on one page.

| Line | Thickness |
| --- | --- |
| `.table-wrap` border-top | **1px solid var(--ink)** (MAX) |
| `thead th` background | — (the row itself carries the header's visual weight) |
| `tbody td` border-bottom | **1px solid var(--line-softer)** (row separator, lighter) |
| `.table-wrap` border-bottom | **1px solid var(--ink)** (same as top) |
| Other list-like components (`.steps`, `.flow`, `.geo-grid`, `.breakdown-list`, `.fee-math`, `.insight-list`) outline | **1px solid var(--ink)** (both top & bottom) |

**Never 2px or more** — a design system violation. (Exception: the 3px `.section-tag` above H2 and the `.part-divider` above H1 are heading dividers, a different layer from the table area, so they are separate.)

#### Component outline patterns — data row (A) vs card (B)

> **A grid component's outline is one of two patterns. Do not mix them.**
> Horizontal grid types all default to Pattern B. Pattern A is restricted to flow components connected by arrows/steps (`.flow`, `.steps`) and tables (`.table-wrap`).

##### Pattern B — self-contained card (default)

Each cell is a self-contained box. Visually separated, giving the impression of floating in a grid.

```css
.problem-grid {
  display: grid;
  gap: 1px;
  background: var(--line-soft);            /* the gap shows through as a line */
  border: 1px solid var(--line-soft);      /* outer box on all sides */
}
.problem-card { background: var(--paper); padding: 32px; }    /* white cards lift off the ivory page */
```

| Applies to |
| --- |
| `.problem-grid`, `.brand-cards` (self-contained insight/profile cards) |
| `.kpi-row`, `.metric-grid`, `.geo-grid` (numeric comparison grids) |

##### Pattern A — data row / flow (exception)

Restricted to components whose meaning is connected by arrows/steps, and to the table body itself. A light tone that blends naturally into the body flow.

```css
.flow {
  display: grid;
  border-top:    1px solid var(--ink);    /* black top 1px */
  border-bottom: 1px solid var(--ink);    /* black bottom 1px */
}
.flow-step { border-left: 1px solid var(--line-soft); }
.flow-step:first-child { border-left: none; }
.flow-step::after { content: "→"; }                   /* arrow between steps */
```

| Applies to |
| --- |
| `.flow`, `.steps` (flows connected by arrows/steps) |
| `.table-wrap` (table body — thead·tbody structure) |

##### Decision criteria

| Content nature | Pattern |
| --- | --- |
| Horizontal comparison data grid (numbers/labels/short descriptions) | **B: card** (default) |
| Each cell is self-contained content (heading+body+stat) | **B: card** |
| **Flow connected by arrows/steps** (process flow, sequential steps) | **A: data row** |
| **Table body** (thead + tbody) | **A: data row** |

**Decision guide**:

- "Is this a card grid or a flow?" — if a flow, A; otherwise B.
- A is only when the meaning of **order/connection** (arrows, numbered steps, etc.) must be carried visually.
- A simple 4-KPI / 4-market comparison is **B**.

### 7.7 PART group header (`.part-divider` / H1)

> **When sections exceed about 6, group them with H1 PART headers.** A flat 1–15 number list makes the eye travel far and lose the flow. PART headers serve as "chapter covers" within the report.

```html
<section class="part-divider" id="part-2">
  <div class="section-inner">
    <div class="part-eyebrow">PART II</div>
    <h1>Domestic Market Analysis</h1>
    <span class="part-meta">Korea Market — from market status to IP licensing</span>
  </div>
</section>
```

```css
/* PART DIVIDER — warm slate band with a clay sheen. Color is limited to .section-inner (body width = --max), matching the body width rather than the full screen */
.part-divider {
  padding: 0 var(--pad-x);                           /* outer: only edge margins on narrow screens */
  margin-top: 120px;
}
.part-divider:first-of-type { margin-top: var(--section-py); }   /* when the first element is a PART, don't stick to the cover — same as a normal section's top padding (72px) */
.part-divider .section-inner {
  max-width: var(--max);                              /* limited to body width = --max */
  margin: 0 auto;
  width: 100%;
  background:
    linear-gradient(120deg, rgba(217, 119, 87, 0.22) 0%, transparent 42%, transparent 62%, rgba(212, 162, 127, 0.12) 100%),
    var(--brand-slate);                               /* warm slate base + diagonal sheen — top-left clay 22% / bottom-right kraft 12% */
  color: var(--brand-ivory);                          /* ivory text on the dark band */
  padding: 44px 40px;
  border-radius: var(--radius);                       /* rounded corners — gives a chapter-card sense of separation */
  overflow: hidden;                                    /* keep the gradient inside the rounded corners */
}
/* PART eyebrow/meta are mono uppercase, letter-spacing 0 */
.part-divider .part-eyebrow {
  font-family: var(--font-mono);
  font-size: 14px;          /* one step above body micro (12px), in tune with H1 (48px) */
  letter-spacing: 0.02em;
  text-transform: uppercase;
  color: rgba(250,249,245,0.72);
  font-weight: 700;
  margin-bottom: 12px;
}
.part-divider h1 { font-family: var(--font-display); color: var(--brand-ivory); letter-spacing: -0.01em; font-weight: 600; }   /* serif headline */
.part-divider .part-meta {
  display: block;
  margin-top: 12px;
  font-family: var(--font-mono);
  font-size: 14px;
  letter-spacing: 0;
  text-transform: uppercase;
  color: rgba(250,249,245,0.72);
  font-weight: 600;
}
```

#### Authoring rules

- **PART numbers** are Roman numerals (`PART I`, `PART II`, `PART III`, …). English mono uppercase.
- **PART titles** are Korean (`Domestic Market Analysis`, `Strategic Implications`, etc.). Use the H1 token (48px).
- **part-meta** is an English subtitle + short description. Mono uppercase.
- If sections are fewer than 6, PART grouping is unnecessary. Even with 6–8, keep a flat structure if a single flow is natural.
- A PART divider is itself exposed as an H1 item in the navigator.

#### Do not use a divider in the appendix (APX) area

- Sub-blocks within an appendix (`APX`) section (e.g., a Phase 1·2·3 roadmap) are separated **by margin only, without a top divider line**.
- Unlike body sections, an appendix is supplementary; a strongly drawn divider is easily misread as body-level weight.

```css
/* APX Phase block — no divider, separated by margin only */
.phase { border-top: none; padding-top: 0; margin-top: 56px; }
.phase:first-child { margin-top: 0; }
```

---

## 8. Callout / Highlight Box — unified section summary box

> **A single class `.callout` serves all "emphasis box" roles.**
> That is, the _Highlight box_, _Key Takeaway box_, _So What box_, and _Implication box_ all use the same structure `.callout` and distinguish their purpose **only by changing the top label text.**

### 8.1 Structure

The base structure is identical for all. Add a modifier class only according to the label.

```html
<!-- default (warm sand): Key Takeaway / So What / Implication / Highlight -->
<div class="callout">
  <div class="lbl">Key Takeaway</div>
  <p>…summary sentence…</p>
</div>

<!-- Note: pale clay -->
<div class="callout callout-note">
  <div class="lbl">Note</div>
  <p>…caution / premise / footnote…</p>
</div>

<!-- Important: pale red -->
<div class="callout callout-important">
  <div class="lbl">Important</div>
  <p>…decisive info you must not miss…</p>
</div>
```

### 8.2 Style

```css
/* Default — warm sand (manila). Used by Key Takeaway / So What / Implication / Highlight alike. No left emphasis bar. */
.callout {
  margin-top: 32px;
  margin-bottom: 0;                                       /* the next sibling's margin determines the gap */
  padding: 24px 28px;
  background: rgba(235, 219, 188, 0.40);                  /* brand-manila 40% — warm sand */
  border-left: none;                                       /* ❗ no left emphasis bar — emphasis via background color only */
  border-radius: var(--radius);                            /* rounded warm card */
}

/* Tone variants — modifier classes swap only the background color (no left bar) */
.callout.callout-note      { background: rgba(217, 119, 87, 0.10); }    /* pale clay */
.callout.callout-important { background: rgba(191, 77, 67, 0.10); }     /* pale warm red */

.callout .lbl {
  font-family: var(--font-mono);
  font-size: var(--fs-micro);            /* 12px */
  text-transform: uppercase;
  color: var(--accent-deep);             /* clay label — the box's one spot of accent */
  margin-bottom: 10px;
  font-weight: 600;
  letter-spacing: 0;                     /* ❗ no letter-spacing — keeps the box label tone calm */
}
.callout p {
  font-size: var(--fs-body);             /* 15px */
  color: var(--ink);                     /* darker black than body — it's an emphasis box */
  line-height: var(--lh-loose);
}
.callout p + p { margin-top: 8px; }
```

### 8.3 Label usage guide (6 types)

| Label | Color | Modifier class | When to use |
| --- | --- | --- | --- |
| `Key Takeaway` | **warm sand (default)** | (none) | The one-line conclusion the section conveys. **Default.** |
| `Highlight` | **warm sand (default)** | (none) | Emphasize outliers / surprising facts in the data |
| `So What` | **warm sand (default)** | (none) | "So what should we do" — action/decision implication |
| `Implication` | **warm sand (default)** | (none) | Ripple effects on market/org/product |
| `Note` | **pale clay** | `.callout-note` | Cautions / premises / footnotes |
| `Important` | **pale warm red** | `.callout-important` | Decisive info you must not miss (use sparingly) |

> Semantic emphasis (summary/highlight/implication/conclusion) all shares the same warm sand (manila) tone as one group. **Use another tone only when the intent is clearly different**: Note is supplementary info (pale clay), Important is risk/warning-level decisive info (pale warm red).
> The left emphasis bar (border-left) is not used in any variant — background color alone provides enough visual identification.

### 8.4 Authoring rules

- **The structure is always identical**: `.callout > .lbl + <p>…`. No variation.
- Color via modifier class only — no inline style.
- **Labels are English uppercase**, **body is Korean**.
- Body is 1–2 paragraphs. If it grows to 3+ paragraphs, move it out to a body section.
- Do not add decorations to the box (triangles, quotes, icons, etc.).
- Use `.callout` **only once** per section. Do not stack two or more (it dilutes the meaning of emphasis).
- Position is usually at the end of the section — appearing as a closing box after all the data/body.

---

## 9. Footer

Light tone + small text (smaller than the header) + a footer version of the header info.

```html
<footer class="footer" role="contentinfo">
  <div class="footer-inner">
    <div class="footer-row">
      <div class="footer-left">
        <div class="footer-line">
          <span class="footer-doc-title">Payment &amp; Coupon Market Analysis</span>
        </div>
        <div class="footer-line footer-line-sub">
          <span>-</span><span class="dot">·</span>
          <span>-</span><span class="dot">·</span>
          <span class="mono">-</span>
        </div>
      </div>
      <div class="footer-right">
        <span class="footer-confidential">CONFIDENTIAL</span>
      </div>
    </div>
    <p class="footer-disclaimer">
      This document is confidential. Access and distribution by anyone other than authorized users is prohibited; violations may result in disciplinary action and civil or criminal liability.
    </p>
    <div class="footer-copyright">© All Rights Reserved.</div>
  </div>
</footer>
```

### 9.1 Footer rules

- Background `--surface` (white), with `border-top: 1px solid var(--line-soft)` on top.
- `padding: 28px var(--pad-x)`. Gap from the last section is `margin-top: 160px`.
- Left: **title (bold, ink) + a one-line meta (small, light ink-3)**.
  - The meta line: **`Team · Name · Date`** (three items, all on one line).
  - **Date format is `YYYY.MM.DD`** (same as the cover, see 5.2). `class="mono"` is required on the date span.
  - **Do not show Version** (see 5.2).
  - **Hide empty meta in the footer** — the cover shows `-`, but the footer's one-line meta is short and an empty slot is more awkward, so **exclude that span itself** (auto-remove via JS, or omit in markup). Also clean up neighboring separators (`·`).
  - `gap: 4px` between items (narrower than the header).

#### JS — auto-hide empty footer meta

```javascript
/* Remove meta spans whose text is `-` inside .footer-line-sub.
   Clean up remaining dots (`·`) at the ends + consecutive ones. Result: clean like `Team · Date`. */
document.querySelectorAll('.footer-line-sub').forEach(line => {
  Array.from(line.children).forEach(el => {
    if (!el.classList.contains('dot') && el.textContent.trim() === '-') el.remove();
  });
  let kids = Array.from(line.children);
  for (let i = kids.length - 1; i >= 0; i--) {
    const el = kids[i];
    if (!el.classList.contains('dot')) continue;
    const p = el.previousElementSibling, n = el.nextElementSibling;
    if (!p || !n || p.classList.contains('dot') || n.classList.contains('dot')) el.remove();
  }
});
```

> **The cover is unchanged.** The three cover meta values (Date · Team · Author) always show three labels in a grid structure, so display `-` in empty slots. The footer is a free-flowing single line where an empty slot looks visually awkward, so hiding is natural.

- Right: **confidential chip** — same design as the cover chip (outline + red dot + uppercase mono).
- Disclaimer is `--fs-micro` (12px), `--ink-4`, max-width 720px.
- Copyright is mono, `--ink-5`, with a thin 1px line above (`var(--surface-1)`, #f7f7f7) — an almost invisible light separator. Even lighter than `var(--line-softer)` (#ededed), so the footer's last line doesn't feel visually floating.

### 9.2 Hierarchy rules

- **Footer text is smaller than or equal to the header (top nav).**
- Only `.footer-doc-title` is ink + bold + `--fs-body-sm` (13px).
- The meta line is `--fs-micro` (12px) + `--ink-3`. Do not use anything too light (below `--ink-5`).

---

## 10. Component Reference

The data/content components used in this report. All follow the black-and-white + one emphasis color principle.

| Component | Class | Use |
| --- | --- | --- |
| KPI Row | `.kpi-row > .kpi` | 4 key metrics laid out horizontally |
| Exec Card | `.exec-card` | executive summary container |
| Bar Chart | `.bar-chart > .bar-row` | horizontal bars by year/item |
| Stack Bar | `.stack > .stack-seg` + `.stack-legend` | composition stacked bar + legend |
| Breakdown List | `.breakdown-list > .bd-row` | label/description/bar/value per row |
| Problem Cards | `.problem-grid > .problem-card` | 3-way insight cards |
| Geo Cells | `.geo-grid > .geo-cell` | 4-country/region comparison |
| Comp Table | `.comp-table` | competitor financial comparison table |
| Brand Cards | `.brand-cards > .brand-card` | domestic player cards |
| Flow | `.flow > .flow-step` | 5-step flow (`→` arrow automatic) |
| Fee Math | `.fee-math > .fee-side` | left/right comparison formula / margin calc |
| Insight List | `.insight-list > .insight-row` | large number + heading + body |

Each component starts/ends with a **1px black line on top and bottom**. Between cells is `--line-soft`.

---

## 11. Motion

```css
--ease: cubic-bezier(0.32, 0.72, 0, 1);   /* iOS-like */
--dur:  240ms;
```

- Transition only color, border, and transform. Do not use heavy motion like opacity fade-ins.
- Enable `html { scroll-behavior: smooth; }`.

---

## 12. Accessibility / Markup Hygiene

- Document language: `<html lang="ko">`.
- Side navigation is `<aside aria-label="Section navigation">`.
- Footer is `<footer role="contentinfo">`.
- Maintain semantic heading hierarchy (h1 → h2 → h3). No heading jumps.
- Do not convey meaning by color alone — deduction/danger/positive always come with a label or sign.

---

## 13. Authoring & Operations Checklist

Check when creating a new report:

- [ ] `<html lang="ko">` set
- [ ] Pretendard CDN loaded **and a serif display font** (Noto Serif KR via Google Fonts) for `--font-display`
- [ ] **Warm palette**: page background is ivory `--surface: #faf9f5` (never `#ffffff`); text is warm brown-black `--ink-2: #3D3929`; the one accent is clay `#D97757` (no blue/cool-gray anywhere)
- [ ] **Cards use `--paper: #fff` fill on the ivory page** (so they lift); rounded via `--radius: 12px` + `overflow:hidden`
- [ ] `word-break: keep-all; overflow-wrap: break-word;` on the body
- [ ] All font sizes use `--fs-*` tokens (nothing under 12px)
- [ ] **Body default width `--max: 800px`** — shared by cover/section/footer, aligned uniformly by one token
- [ ] **`--max` alignment handled by `.section-inner`/`.cover-inner`/`.footer-inner`** — don't put `max-width` and padding together on `main` (it narrows the body and misaligns from cover/footer)
- [ ] **No fixed top bar (top nav)** — navigation is the side nav only
- [ ] **Side nav fixed on the body's left** — `left: max(24px, calc(50% - (--max/2) - 40px - 200px))`
- [ ] **TOC display range ≥1500px**, hidden below (with an 800px body, always a 40px gap with no transition range)
- [ ] **Include the Scroll-to-Top floating button (`.scroll-top`)** — fixed bottom-right, shown after 600px scroll
- [ ] Cover: eyebrow (English) + title (Korean) + summary (2–3 lines, cover-only) + confidential chip + **3 meta** (Date / Team / Author)
- [ ] **Display `-` for empty meta values**, no Version
- [ ] **Dates in `YYYY.MM.DD` format** (e.g., `2025.05.04`) — both cover and footer. Apply mono (`class="mono"`)
- [ ] Side nav items: static noun-form titles + two-digit numbers
- [ ] Section lede is **1–2 paragraphs** (follows body width) · no triple duplication of one-line summary + body + callout
- [ ] **`section-tag` is exactly one line** (no text inside)
- [ ] **Section head is H2 + lede only** — no English meta label to the right of the title
- [ ] **Heading line rule: only H1 & H2 have a line.** H3 & H4 have no line (never add a `.block-head` border)
- [ ] **Heading margin scale: H1(120) > H2(72) > H3(56) > H4(36)** — shrinking by hierarchy. Even H4 is well separated from body
- [ ] **H1/H2 are serif (`--font-display`, weight 600); H3/H4 stay sans (Pretendard, weight 700)** — the serif/sans switch at H2→H3 carries the Claude voice
- [ ] **All H2 unified to serif 40px / weight 600** (`--fs-h2` token), H1 is serif 48px — ignore other classes like `display-xl` (force via CSS `!important`)
- [ ] **`.num-prefix` is mono + clay accent** — the one spot of accent color in the section head, before the serif title
- [ ] **Single rule for section vertical rhythm**: `.section-inner > * { margin-top: 56px }`, inside grids `.g2 > *, .g3 > * { margin-top: 0 }` — no component's own margin
- [ ] **`.callout` margin-bottom: 0** — the next sibling's margin-top determines the gap (avoids double-adding)
- [ ] **Group with H1 PART headers if there are 6+ sections** (`.part-divider`)
- [ ] **Side nav shows only two hierarchies, H1 & H2** — H1 is prominent via the `.sn-h1` class, H2 is indented
- [ ] **Wrap title+component (table/chart/KPI) together with `.block`** — the title attaches to the table at 24px, separated from the outer 56px section rhythm. Placing them as direct siblings opens a 56px gap
- [ ] **Choose one of 2 subheading patterns**: A) `<h3>` 20px no-line (default) / B) `.block-head h3` 20px no-line (H3 + right-side meta wrapper). **A title above a data component like table/chart/KPI is always H3** (no demotion to H4)
- [ ] **No horizontal (g2) for two blocks that include a table** — stack vertically
- [ ] **Attach `class="num"` to both header and cells of every numeric column** consistently
- [ ] **All table/list-type component outlines are 1px MAX** (`.table-wrap` · `.steps` · `.flow` · `.geo-grid`, etc.) — no 2px+
- [ ] **Separate the appendix (APX) area by margin only, without a divider** (remove `.phase` border-top)
- [ ] **Serif display (H1/H2/cover title) takes light tracking `-0.01em ~ -0.02em`**; sans H3/H4 · number prefixes · small labels stay letter-spacing 0 — positive letter-spacing only on cover/footer English chips
- [ ] **PART divider (`.part-divider`) is a warm-slate band + clay 22% sheen + `--radius`** — a chapter-cover effect via color fill instead of a thick line fill
- [ ] **Callout default is warm sand (manila 40%)**; Note = pale clay, Important = pale warm red; label text is clay
- [ ] **H3 margin rule uses a descendant selector (`.section-inner h3`)** — applied consistently to h3 at any depth, `:first-child` is 0
- [ ] Every section's closing summary uses the single `.callout` pattern
- [ ] Footer: title (bold) + one-line meta (team · name · date) + confidential chip + disclaimer + copyright
- [ ] Last section ↔ footer `margin-top: 160px`
- [ ] No interrogative headings ("...?")

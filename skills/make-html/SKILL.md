---
name: make-html
description: Generate editorial-tone HTML reports that follow this design system's rules. Use only when the user explicitly requests HTML report generation, e.g. "HTML 보고서로 만들어줘", "리포트 형식으로", "이 디자인시스템으로", "이 PDF/자료를 보고서로 변환해줘". Do not apply for simple questions, summaries, read-only requests, or when only a data table is needed.
---

# make-html — HTML Design System

A skill that captures the design rules (color tokens, typography, cover, side nav, sections, callouts, footer) to follow when building report HTML.

**Visual language: the Anthropic / Claude warm-editorial skin** — the look you get when you ask Claude to generate an HTML report: a warm ivory canvas (never pure white), warm brown-black ink (never cool gray), a single terracotta **clay** accent (`#D97757`, never blue/slate), serif display headlines over a Pretendard sans body, and gently rounded warm cards.

## When to Apply — READ FIRST

Apply this design system **only when the user explicitly requests HTML report generation.**

- ✅ Apply: "make it an HTML report", "in report format", "with this design system", "convert this PDF/material into a report", or when continuing to write the same report from an earlier conversation.
- ❌ Do not apply: simple Q&A, summaries/notes, read-only requests ("read it for me / tell me / check it"), data/table-only needs, code review/debugging, or when another format (PPT, DOCX, Markdown, etc.) is specified.
- If ambiguous, ask: "Should I make this an HTML report, or organize it as text?"

## Two Modes — pick one before generating

Both modes share the **same warm palette + serif/sans typography**; they differ only in skeleton (chrome).

- **Report mode** (heavy) — cover + side nav + PART dividers + footer. For analysis, planning, PRD, data-heavy decks.
- **Lite / Article mode** (light) — a single readable 780px column with just a title header. **The default for prose: translations, essays, letters, articles, notes.** No cover, no side nav, no PART, no footer.

**Selection (auto + explicit hybrid):**
1. Explicit request wins — "가볍게 / 아티클 / lite / 문서로" → Lite; "보고서 / 리포트 / 발표자료" → Report.
2. Otherwise auto-detect: prose-like input (a translation, essay, letter, article) → **Lite**; structured/analytical input → **Report**.
3. Unsure → default to Lite or ask.

> ⚠️ Asking to "translate this into HTML" is a **Lite** job. Never wrap a translation in a cover / side nav / PART / footer. See design-system.md §14 for the lite skeleton and CSS.

## How to Use

1. **Read the full ruleset first.** Before generating, read [references/design-system.md](references/design-system.md) from start to finish. Color tokens, the type scale, layout tokens, and component markup are all defined there; use only the defined tokens and never arbitrary values.
2. **Reference the example.** Check the finished output shape in [assets/example-service-prd.html](assets/example-service-prd.html). It contains the full structure (cover → side nav → sections → callouts → footer) and real CSS usage.
3. **Output a single HTML file.** Inline the CSS in `<style>` and produce a single self-contained `.html` file with no external dependencies.
4. **Verify with the checklist.** After finishing, go through "13. Authoring & Operations Checklist" in design-system.md item by item.

## Core Principles (Summary)

- Warm, not clinical — ivory canvas `#faf9f5` (never `#ffffff`), warm brown-black ink `#3D3929` (never cool gray). This warmth is the whole point of the skin.
- Editorial tone — a literary-journal tone, not a marketing page. Minimize heavy shadows; favor ink + soft warm lines + gentle rounded corners (`--radius: 12px`).
- Typography first — **serif display headlines** (cover title / PART H1 / section H2) over a **Pretendard sans body**; the type scale comes before components.
- One accent = clay — the single emphasis color is terracotta `#D97757`. Limit color emphasis to 1–2 times per page; the default is the `--ink` family. Never add a second accent hue.
- Numbers must be crisp — apply `font-feature-settings: "tnum"` to all numeric text.
- Don't fear whitespace — generous section spacing.
- Korean requires word-level line breaking (`word-break: keep-all`).

For the detailed rules, tokens, and full markup, see references/design-system.md.

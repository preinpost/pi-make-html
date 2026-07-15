---
name: make-html
description: Generate editorial-tone HTML reports that follow this design system's rules. Use only when the user explicitly requests HTML report generation, e.g. "HTML 보고서로 만들어줘", "리포트 형식으로", "이 디자인시스템으로", "이 PDF/자료를 보고서로 변환해줘". Do not apply for simple questions, summaries, read-only requests, or when only a data table is needed.
---

# make-html — HTML Design System

A skill that captures the design rules (color tokens, typography, cover, side nav, sections, callouts, footer) to follow when building report HTML.

## When to Apply — READ FIRST

Apply this design system **only when the user explicitly requests HTML report generation.**

- ✅ Apply: "make it an HTML report", "in report format", "with this design system", "convert this PDF/material into a report", or when continuing to write the same report from an earlier conversation.
- ❌ Do not apply: simple Q&A, summaries/notes, read-only requests ("read it for me / tell me / check it"), data/table-only needs, code review/debugging, or when another format (PPT, DOCX, Markdown, etc.) is specified.
- If ambiguous, ask: "Should I make this an HTML report, or organize it as text?"

## How to Use

1. **Read the full ruleset first.** Before generating, read [references/design-system.md](references/design-system.md) from start to finish. Color tokens, the type scale, layout tokens, and component markup are all defined there; use only the defined tokens and never arbitrary values.
2. **Reference the example.** Check the finished output shape in [assets/example-service-prd.html](assets/example-service-prd.html). It contains the full structure (cover → side nav → sections → callouts → footer) and real CSS usage.
3. **Output a single HTML file.** Inline the CSS in `<style>` and produce a single self-contained `.html` file with no external dependencies.
4. **Verify with the checklist.** After finishing, go through "13. Authoring & Operations Checklist" in design-system.md item by item.

## Core Principles (Summary)

- Editorial tone — a publication tone, not a marketing page. Minimize gradients and shadows; favor black ink + lines.
- Typography first — the type scale comes before components. All text uses the defined tokens.
- One emphasis — limit color emphasis to 1–2 times per page. The default is all `--ink` family.
- Numbers must be crisp — apply `font-feature-settings: "tnum"` to all numeric text.
- Don't fear whitespace — generous section spacing.
- Korean requires word-level line breaking (`word-break: keep-all`).

For the detailed rules, tokens, and full markup, see references/design-system.md.

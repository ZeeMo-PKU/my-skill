---
name: chinese-pdf-explainer
description: Explain academic PDFs, paper links, file paths, and article URLs in Chinese. Use when the user provides a PDF path, PDF upload, arXiv/DOI/publisher link, or article link and asks for translation, explanation, summary, evaluation, or relation to their current project.
---

# Chinese PDF Explainer

## Purpose

Help the user read academic PDFs or article links in Chinese while preserving the original meaning. Produce metadata, section-by-section or paragraph-by-paragraph original text, faithful translation, local summaries, whole-paper summary and evaluation, and relevance to the user's active project.

Use prior conversation context when discussing project relevance. For this user, likely project context may include MyGO, compiler research, architecture, EDA, LLM inference systems, and advisor/lab research. Clearly distinguish paper facts from your inference.

## Source Handling

1. For a local PDF path or uploaded PDF, inspect the document directly.
2. For a URL, open the official paper page or PDF when possible. Prefer publisher, arXiv, DOI, conference, or author pages over third-party mirrors.
3. If the file is long, avoid translating the entire paper at once unless the user explicitly asks. Process by abstract, introduction, method, experiment, and conclusion, or by the requested pages/sections.
4. If the PDF text extraction is poor, say so and rely on visible text, OCR, screenshots, or metadata as available.

## Metadata Header

Start every response with a paper header:

```markdown
**Paper Header**
- Link: [source URL or local file path]
- Title: [paper title]
- Authors: [authors]
- Venue / Publication: [conference, journal, arXiv, preprint, thesis, unknown]
- Year / Date: [year or date]
- DOI / arXiv ID: [if available]
```

If a field is unavailable, write `Unknown` rather than guessing.

## Main Explanation Format

For each paragraph or section, use:

```markdown
**Section / Paragraph**

Original:
[English original text]

Translation:
[Faithful Chinese translation]

Local Summary:
[What this paragraph/section is doing and its key point]
```

Choose paragraph-level output for short excerpts and section-level output for long PDFs. If summarizing by section, include representative original sentences for key claims rather than dumping excessive text.

## Whole-Paper Closing

End with:

```markdown
**Whole-Paper Summary**
[Problem, method, evidence, conclusion]

**Evaluation**
[Strengths, limitations, credibility, novelty, and what to verify]

**Relation to Your Current Project**
[Concrete implications for the user's current project. Mark inference clearly.]
```

## Fidelity Rules

- Preserve claim strength, scope, conditions, and uncertainty.
- Keep key technical terms in English with Chinese explanation on first use.
- Do not convert "may", "can", "suggests", or "we observe" into stronger claims.
- Preserve comparison targets and metrics.
- Do not invent venue, authors, methods, results, or project relevance.
- If a passage is ambiguous, explain the ambiguity and what context would resolve it.

Read `references/fidelity-checklist.md` when translating dense academic text, when evaluating a paper, or when the user is worried about meaning drift.

## Style

Write the answer in Chinese by default. Keep the English original text in the paragraph/section blocks. Be concise but complete enough for academic reading. Prefer accurate translation over polished paraphrase.

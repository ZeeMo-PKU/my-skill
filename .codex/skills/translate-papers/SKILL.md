---
name: translate-papers
description: Translate and explain academic English papers while preserving meaning. Use when the user provides an English academic paragraph, paper PDF, arXiv/DOI/publisher link, or paper excerpt and asks for translation, explanation, reading help, or implications for their current project or prior discussion.
---

# Translate Papers

## Core Rule

Treat translation as scholarly reading support, not as free paraphrasing. Preserve claims, scope, uncertainty, comparison targets, and technical terms. Do not make the paper sound stronger, broader, or more certain than the original.

Use the prior conversation and the user's active project context when explaining implications, but clearly separate what the paper says from your inference.

## Workflow

1. Identify the source type.
   - For pasted text, work directly from the provided excerpt.
   - For PDFs or links, inspect the paper metadata, abstract, surrounding section, and relevant figures/tables when available.
   - If the excerpt depends on prior context, read enough surrounding text to avoid mistranslating references such as "this approach", "our system", or "these results".

2. Build a lightweight context before translating.
   - Identify the paper topic, section, local argument, and key technical terms.
   - Reuse terminology from earlier turns when the user has an active project, such as MyGO, compiler research, architecture, EDA, LLM serving, or advisor/lab research.

3. Translate faithfully.
   - Keep the original English text in the answer.
   - Provide a close Chinese translation before the explanation.
   - Preserve hedging words such as "may", "can", "suggests", "we observe", "up to", "under", and "in our experiments".
   - Preserve logical relations such as cause, contrast, condition, limitation, and comparison.
   - Keep standard technical terms in English when a Chinese translation would be ambiguous; provide the Chinese meaning after the first mention.

4. Explain the excerpt.
   - State what this passage is doing in the paper: motivation, method, assumption, result, limitation, related work, or contribution.
   - Summarize the main point in plain Chinese.
   - Identify highlights, novelty, or why the authors include this passage.

5. Connect to the user's project.
   - Explain concrete implications for the user's project or research direction.
   - Mark project implications as inference when they are not explicitly stated in the paper.
   - Prefer actionable connections: what to learn, what to compare, what experiment to run, what vocabulary to reuse, or what risk to avoid.

6. Check for meaning drift.
   - Before finalizing, verify claims against the original wording.
   - If uncertain about a term or context, say what is uncertain and what context would resolve it.
   - Use `references/reading-checks.md` for common academic-reading checks when the passage is dense or important.

## Output Format

Use this structure by default:

```markdown
**Direct Translation**
[Faithful Chinese translation.]

**Original English**
[Original excerpt, preserving paragraph order.]

**Summary**
- Function in the paper: [motivation/method/result/etc.]
- Main point: [plain Chinese summary]
- Highlights: [what is important or novel]

**Implications for Your Project**
[Concrete implications connected to the user's project and prior conversation. Clearly label inference.]

**Terms / Caution Points**
[Key terms and likely mistranslation risks, only when useful.]
```

For long PDFs or full papers, summarize the paper first, then translate the requested section. Do not translate a whole paper unless the user explicitly requests a full-document workflow.

## Style

Use Chinese for explanations unless the user asks otherwise. Keep the tone direct and study-oriented. Prefer accurate, slightly literal translation over polished but loose translation. When a sentence is structurally difficult, briefly explain the grammar or clause structure.

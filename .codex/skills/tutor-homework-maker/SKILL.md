---
name: tutor-homework-maker
description: Use when the user asks Codex to design, generate, revise, or package Chinese tutoring homework, practice sets, quizzes, exam-style worksheets, student PDFs, or answer sheets based on declared subject, difficulty, quantity, question type, textbook pages/chapters, exercise books, PDFs, images, or prior examples. The skill supports configurable difficulty, number of questions, type mix, subject, reference教材/习题册, student-only versions, answer versions, and PDF/Markdown/Word-style deliverables.
---

# Tutor Homework Maker

## Core Workflow

1. Confirm the assignment parameters.
   - Extract subject, grade/book version, chapter or page range, difficulty, question count, question types, and whether answers are needed.
   - Accept terse user prompts such as "第四章，20题，19个单选1个大题，中等为主，参考这个PDF".
   - If a required parameter is missing, make a reasonable default when safe; ask only when the subject/range or output form is ambiguous enough to change the work.

2. Read reference materials before writing questions.
   - For PDFs, inspect the relevant chapter/page range and identify concepts, formula patterns, example style, and problem wording style.
   - For images or screenshots, use visual inspection when text extraction is incomplete.
   - For exercise books, mimic topic coverage and difficulty distribution, but do not copy long original question text unless the user explicitly asks to extract existing questions.
   - Record the exact source file paths and selected chapters/pages in working notes or the generated artifact when useful.

3. Build a brief blueprint before generating.
   - Allocate question types and difficulty, for example "13 single-choice basic, 2 calculation questions".
   - Cover the key knowledge points in the requested range without overconcentrating on one section.
   - Include a small number of mixed or synthesis questions only when the user requests medium/hard work.
   - Keep the set suitable for tutoring: clear wording, solvable with the referenced materials, and not overloaded with trick questions unless requested.

4. Generate the student version.
   - Use Chinese by default.
   - Number questions consecutively.
   - For single-choice questions, provide four options A-D unless the user asks otherwise.
   - For fill-in/short-answer/calculation questions, leave enough visible answer space in PDF/Word-style outputs.
   - Do not include answers in the student version unless the user asks for answers inline.
   - Avoid visible meta text like "难度：中等" inside the student worksheet unless the user wants it; title and scope are enough.

5. Generate the answer version when requested.
   - For objective questions, include the correct option and one-sentence reasoning.
   - For calculation/proof/large questions, include key steps, formulas, substitutions, and final result.
   - Keep explanations concise enough for a tutor to use quickly.
   - If the user says "不需要参考答案", do not generate or append answer content.

6. Package deliverables.
   - If the user asks for PDF, create a student PDF and, when requested, a separate answer PDF.
   - If the user asks for quick output, Markdown is acceptable.
   - Save generated files in the user's requested folder; otherwise use the active thread outputs folder or the same folder as the source material when that matches the user's wording.
   - Use stable Chinese filenames such as `第4章作业_学生版.pdf` and `第4章作业_参考答案.pdf`.

7. Validate before final response.
   - Check the generated count matches the requested quantity and type mix exactly.
   - Check answer keys match generated options.
   - Check formulas, units, and known facts against the reference material.
   - For PDFs, render or inspect enough pages to make sure Chinese text, line breaks, question numbers, and answer spaces are readable.

## Parameter Handling

Use these defaults unless the user says otherwise:

- Subject: infer from the reference material or prompt.
- Difficulty: basic to medium if unspecified.
- Quantity: infer from prompt; if absent, ask.
- Types: follow prompt exactly; if absent, choose a balanced mix for the subject.
- Scope: use stated chapter/page range; if absent and a source file is given, ask before generating.
- Answers: do not include answers unless requested or the user asks for "答案版/参考答案/解析".
- Originality: create new questions inspired by the material; do not copy from copyrighted教材/习题册 at length.

## Difficulty Rules

- Basic: direct concept recognition, formula substitution, one-step calculation, common examples from the textbook.
- Medium: two-step reasoning, concept comparison, graph/table interpretation, parameter changes, standard exam variants.
- Hard: synthesis across sections, non-obvious constraints, multi-step calculation, reverse reasoning, or distractors that target common misconceptions.
- Mixed: state an internal distribution, such as 70% medium and 30% hard, then generate accordingly.

## Subject Notes

- Physics: emphasize physical meaning, conditions of formulas, units, diagrams described in words when no image is needed, and avoid impossible numerical values.
- Math: include clean expressions, exact answer forms, and proof/calculation steps when answers are generated.
- Chemistry: balance equations, charge conservation, units, and experimental conditions.
- English/Chinese: separate reading material, prompts, and answer keys clearly; avoid answer leakage in student versions.

## Final Response

Report only what matters:

- What was generated.
- Exact file paths with absolute links when files were saved.
- Whether a student version and answer version were created.
- Any parameter assumption, missing reference range, or validation limitation.

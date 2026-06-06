---
name: device-course-report
description: Use when the user asks Codex to write, revise, complete, or package a Chinese device-course project report, especially LaTeX or Markdown reports based on an assignment PDF, experiment results, screenshots, image folders, TCAD/RO/semiconductor device workflows, or Overleaf image-path issues. The skill covers extracting requirements, answering thought questions, inserting figures, producing .md/.tex/PDF artifacts, and adapting paths for local XeLaTeX or online LaTeX.
---

# Device Course Report

## Core Workflow

1. Gather the source materials.
   - Read the assignment PDF first; extract every task, thought question, formula, required artifact, and note such as "include project path" or "do not modify model".
   - List the image/result directory with `rg --files` or `Get-ChildItem -Recurse`.
   - Inspect representative images, especially screenshots of code/output tables, because numeric results may only be visible in images.
   - If an existing draft is provided, preserve useful structure and fill gaps instead of rewriting blindly.

2. Build a requirement checklist before writing.
   - Map each assignment item to a report section.
   - Include all "思考题/请分析/注意事项".
   - Record project paths and output paths exactly.
   - Separate measured/screenshot results from inferred explanation.

3. Write in Chinese with operational detail.
   - Explain semiconductor/device concepts plainly but technically: what was simulated, what was extracted, why it matters.
   - Use formulas where the assignment gives formulas, then connect them to the actual results.
   - For benchmark reports, include concrete pass/fail or numeric breakdowns when available.
   - For this user's reports, prefer durable artifacts over chat-only answers.

4. Insert figures with stable paths.
   - For local deliverables, prefer copying figures next to the report under an ASCII `figures/` directory and referencing `figures/name.png`.
   - For Overleaf or existing online projects, match the uploaded file tree exactly, for example `图片资源/python代码.png`, `图片资源/任务2/ori_PP.png`, or `图片资源/RO性能/ori_RO性能.png`.
   - Preserve filename case exactly; Overleaf is case-sensitive.
   - Avoid absolute Windows paths inside LaTeX deliverables unless the user explicitly wants local-only compilation.

5. Generate the requested artifact.
   - If the user asks for Markdown containing LaTeX, save a `.md` with complete LaTeX source.
   - If the user asks to "打开 latex 填入" or needs compilation, also create `.tex` and compile with XeLaTeX.
   - Put user-facing deliverables in the active thread's `outputs/` unless the user names another location.
   - If the user asks to save to desktop or a project folder, save there as requested.

6. Validate.
   - Check all `\includegraphics{...}` files exist relative to the compile directory or Overleaf tree.
   - Compile twice with `xelatex` when local compilation is possible.
   - Prefer XeLaTeX for Chinese reports using `ctexart`.
   - Report any unverified assumption or missing input clearly.

## LaTeX Defaults

Use this base unless the user's draft already has stronger constraints:

```latex
\documentclass[UTF8,a4paper,12pt]{ctexart}
\usepackage{graphicx}
\usepackage{geometry}
\usepackage{hyperref}
\usepackage{subcaption}
\usepackage{amsmath}
\usepackage{amssymb}
\geometry{left=2.5cm,right=2.5cm,top=2.5cm,bottom=2.5cm}
\emergencystretch=3em
\hypersetup{colorlinks=true,linkcolor=black,urlcolor=blue,citecolor=blue}
\IfFontExistsTF{Microsoft YaHei}
  {\setCJKmainfont{Microsoft YaHei}}
  {\setCJKmainfont{FandolSong-Regular}}
```

Avoid `\usepackage{float}` unless it is known to be installed. Prefer `[!htbp]` for figures instead of `[H]`.

Use a reusable two-image macro when many comparison figures are needed:

```latex
\newcommand{\twopics}[6]{
\begin{figure}[!htbp]
  \centering
  \begin{subfigure}{0.48\linewidth}
    \centering
    \includegraphics[width=\linewidth]{#1}
    \caption{#2}
  \end{subfigure}
  \hfill
  \begin{subfigure}{0.48\linewidth}
    \centering
    \includegraphics[width=\linewidth]{#3}
    \caption{#4}
  \end{subfigure}
  \caption{#5}
  \label{#6}
\end{figure}
}
```

## Standard Report Structure

Use the assignment's task numbering as section titles. A typical report contains:

- title, authors, date, table of contents
- task 1: workflow explanation and conceptual thought questions
- task 2: script/code completion, formulas, extracted metrics, PP curve
- task 3: parasitic/load influence analysis, comparison figures/tables, thought questions
- statement: local project path, tool template path, output path, constraints followed
- references when requested or useful

For numeric screenshot results, include a short table:

```latex
\begin{table}[!htbp]
  \centering
  \caption{...}
  \begin{tabular}{lccc}
    \hline
    指标 & 原始结构 & 对比结构 & 变化趋势 \\
    \hline
    ...
    \hline
  \end{tabular}
\end{table}
```

## Device/RO Analysis Patterns

For ring oscillator reports, include these reasoning patterns when applicable:

- Dynamic power/current does not need normalization by `Nstage` because more stages increase total switched capacitance but lower oscillation frequency; static current from an inactive/open chain should be divided by `Nstage` to get per-stage average leakage.
- Static RO leakage should be matched at off-state high `VDS`, e.g. `Id(VGS=0,VDS=VDD)`, not at linear-region/low-`VDS` leakage, because inactive CMOS stages hold off devices near supply voltage and high-field effects such as DIBL/GIDL matter.
- If `Ioff,N` and `Ioff,P` differ strongly, compute `IDDQ` as a weighted average over the number of stages where the off nFET or off pFET dominates.
- `Reff=VDD/Ieff` and `Ceff=delay/(ln2*Reff)` are circuit-level extracted effective quantities. They are not purely the physical parasitic resistance or capacitance; BEOL R and C can affect both through coupled RC delay and dynamic current.
- MOL parasitics are inside/near the standard cell; BEOL parasitics are inter-cell routing parasitics; both become more important with scaling because intrinsic device delay shrinks while contact/interconnect resistance and coupling capacitance do not scale ideally.

## Overleaf Path Repair

When the user shows an Overleaf error like `Unable to load picture ... figures/...`:

1. Read the visible file tree or ask for it if unavailable.
2. Replace local copied paths with Overleaf's actual uploaded paths.
3. Keep Chinese paths if Overleaf displays them and the files are uploaded there.
4. Remind the user to select XeLaTeX.
5. Add font fallback with `\IfFontExistsTF` so Overleaf does not fail on `Microsoft YaHei`.

Common mapping from this course project:

```text
figures/python_code.png -> 图片资源/python代码.png
figures/ori_pp.png -> 图片资源/任务2/ori_PP.png
figures/our_pp.png -> 图片资源/任务2/our_PP.png
figures/without_mol_pp.png -> 图片资源/任务2/without_mol_PP.png
figures/without_beol_pp.png -> 图片资源/任务2/无BEOL寄生_pp.png
figures/pp_compare.png -> 图片资源/任务2/对比图.png
figures/ori_ro_performance.png -> 图片资源/RO性能/ori_RO性能.png
figures/without_mol_ro_performance.png -> 图片资源/RO性能/without_mol_RO性能.png
figures/without_beol_ro_performance.png -> 图片资源/RO性能/without_BEOL_RO性能.png
```

## Final Response

Link the saved deliverables with absolute file links. State what was generated, where it was saved, and whether XeLaTeX compilation succeeded. If the user needs Overleaf, provide the exact path-fixed `.tex` or inline code when asked.

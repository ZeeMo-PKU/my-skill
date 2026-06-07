# my-skill

Consolidated personal Codex skill repository.

Skills live under `.codex/skills/<skill-name>`.

## Included Skills

- `academic-paper-to-slides`
- `agent-reach`
- `aspnet-core`
- `chatgpt-apps`
- `chinese-pdf-explainer`
- `cli-creator`
- `cloudflare-deploy`
- `define-goal`
- `device-course-report`
- `figma`
- `figma-code-connect-components`
- `figma-create-design-system-rules`
- `figma-create-new-file`
- `figma-generate-design`
- `figma-generate-library`
- `figma-implement-design`
- `figma-use`
- `figure-extraction`
- `figure-generation`
- `gh-address-comments`
- `gh-fix-ci`
- `hatch-pet`
- `jupyter-notebook`
- `linear`
- `migrate-to-codex`
- `nature-writing`
- `netlify-deploy`
- `notion-knowledge-capture`
- `notion-meeting-intelligence`
- `notion-research-documentation`
- `notion-spec-to-implementation`
- `openai-docs`
- `pdf`
- `playwright`
- `playwright-interactive`
- `render-deploy`
- `screenshot`
- `security-best-practices`
- `security-ownership-map`
- `security-threat-model`
- `sentry`
- `speech`
- `transcribe`
- `translate-papers`
- `tutor-homework-maker`
- `vercel-deploy`
- `winui-app`
- `yeet`

## Install

```sh
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py --repo ZeeMo-PKU/my-skill --path .codex/skills/<skill-name>
```

See `skills-manifest.json` for source tracking.

## Submodules

- `nature-writing` is tracked as a git submodule from `SyntaxSmith/nature-writing-skill` at commit `c1a8716047b6304d922b9528a18421203e3e7acc`. This preserves the upstream source and avoids mixing its no-LICENSE content into this repository's license grant.

When cloning this repository, initialize submodules with:

```sh
git submodule update --init --recursive
```

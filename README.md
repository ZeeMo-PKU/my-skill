# my-skill

Personal Codex skill mirror for the TokenSlides paper-to-slides workflow.

Upstream source:

- https://github.com/pku-lemonade/TokenSlides

Included skills:

- `academic-paper-to-slides`
- `figure-extraction`
- `figure-generation`

Install into Codex from this repository:

```sh
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo ZeeMo-PKU/my-skill \
  --path .codex/skills/academic-paper-to-slides .codex/skills/figure-extraction .codex/skills/figure-generation
```

The copied upstream files are licensed under the Apache License 2.0 as provided by the upstream repository.

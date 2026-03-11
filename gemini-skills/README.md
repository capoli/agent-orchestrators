# Gemini Skills

This repository packages Gemini CLI Agent Skills adapted from Anthropic's official Claude plugins for three workflows:

- `frontend-design`
- `feature-dev`
- `code-review`

Each skill is a top-level directory with a `SKILL.md`, so Gemini CLI can discover them when the repo is linked as a skills source.

## Usage

From this repository, link the skills into Gemini CLI:

```bash
gemini skills link .
```

Gemini will discover the top-level skill folders automatically.

The root [GEMINI.md](./GEMINI.md) provides persistent workspace guidance for design, development, and review work. The skills add deeper workflow guidance when the task matches one of the three areas.

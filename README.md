# article-visual-planning

Decide whether an article needs visuals, what kind they should be, and how they should be produced.

This repo contains a Codex skill focused on editorial decision support, not blind image generation.

It analyzes an article draft and helps answer:

- does this section need a visual at all
- what job should that visual do
- which visual class fits best
- should AI help with structure, prompts, or only planning
- what must be done manually by the author

The skill can also provide:

- diagrams the assistant can generate directly
- image prompts for external image models
- screenshot or manual-capture guidance for the author
- screenshot enhancement guidance
- data or reference visualizations for metrics, comparisons, and quote cards
- cover image direction for article distribution

## Repo layout

```text
skill/article-visual-planning/
  SKILL.md
  agents/openai.yaml
  examples/
    sample-article.en.md
    sample-article.zh-CN.md
    sample-output.en.md
    sample-output.zh-CN.md
  references/
    illustration-taxonomy.md
    prompt-patterns.md
```

## Core idea

The skill treats article visuals as an editorial planning problem:

- first decide whether to add a visual
- use diagrams for structure
- use charts or cards for numbers and comparisons
- use prompts for abstract support images
- use screenshots for proof and authenticity
- use screenshot enhancement when a raw screenshot is not enough
- treat cover images separately from body visuals
- skip visuals when they do not improve comprehension

See `/skill/article-visual-planning` for the publishable skill.

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

But by default, the deliverable is a text plan, not a batch of generated SVG or PNG assets.

## Trigger style

This skill should work with short, natural requests. The user should not need to write a long control prompt every time.

Requests like these should trigger it by default:

- analyze article visuals
- recommend visuals for this post
- generate article visual suggestions
- how should this article be illustrated
- suggest a cover and body visuals for this blog post

Here, "generate" should still default to "generate the recommendation document", not "start producing SVG or PNG files".

## Output shape

The skill now defaults to a per-image output shape instead of a dense recommendation dump.

Each visual is presented as its own block so the reader can immediately see:

- where the image should go
- how important it is
- how it should be produced
- what the image should show
- why it is worth making
- how to make it quickly
- and, only when useful, the prompt or brief

Example:

```md
## Image 1 Cover visual

Put it at: the article opening
Priority: must
Production method: AI image prompt
Recommended visual: an editorial scene showing article-illustration decision making
Why: this sets the topic and tone immediately
Execution: make a horizontal hero image with title-safe space
Prompt or brief: ...
```

This makes the output easier to scan and, more importantly, makes the production decision explicit: author screenshot, screenshot plus annotation, AI-generated diagram, or external image prompting.

## Default delivery mode

This skill should usually unblock the user quickly:

- default to a Markdown visual plan
- if the user asks to save into the article directory, write a text plan file first
- only enter asset generation when the user explicitly asks for `svg`, `png`, Mermaid, a rendered cover, or another concrete visual artifact
- even if the user says "recommend and generate", treat that as "generate the recommendation output" unless the requested artifact type is explicit

This keeps the planning step fast and prevents the skill from getting stuck generating large assets before the article guidance is ready.

If you want to inspect the full example flow, start here:

- Sample article: `/Users/fri/Desktop/my-skills/article-visual-planning/examples/sample-article.en.md`
- Sample output: `/Users/fri/Desktop/my-skills/article-visual-planning/examples/sample-output.en.md`

## Repo layout

```text
.
  SKILL.md
  agents/
    openai.yaml
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

## Production method is explicit

Each recommendation should clearly name one production path:

- author screenshot
- author screenshot + light annotation
- AI-generated diagram
- AI image prompt
- no illustration needed

See `/Users/fri/Desktop/my-skills/article-visual-planning/SKILL.md` for the publishable skill.

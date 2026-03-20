---
name: article-visual-planning
description: Analyze an article, blog post, newsletter draft, or long-form outline and make editorial illustration decisions before any image is produced. Use when Codex needs to judge whether a section should have a visual at all, what job that visual should do, which visual class fits best, whether it should be a diagram, chart, abstract support image, real screenshot, screenshot enhancement, or cover image, and whether the author must create it manually. This skill is primarily for visual planning and decision support, not for directly generating final images, though it may provide prompts or briefs when helpful.
---

# Article Visual Planning

Turn article structure into a practical visual decision plan. Focus on reader comprehension, production feasibility, and platform fit instead of suggesting decorative images everywhere.

If the article already contains visual placeholders or constraints, honor them first. Otherwise, infer the minimum set of visuals that will materially improve understanding.

Treat this skill as an editorial advisor:

- first decide whether a visual is needed
- then decide what kind of visual would help
- then decide who should make it and how
- only then provide prompts or production guidance

## Workflow

### 1. Read for publishing intent

- Identify the article type: tutorial, experience write-up, concept explanation, comparison, announcement, or case study.
- Identify the audience and publication surface if known.
- Estimate how visually dense the piece should be. Default to a light plan, not a maximal one.

### 2. Extract candidate visual slots

- Look for sections that introduce a workflow, taxonomy, comparison, turning point, tool UI, metric, or abstract concept.
- Suggest fewer visuals when the article is already highly concrete.
- Merge overlapping slots so the plan stays realistic.
- Default target: 3-5 visuals for a typical 4k-7k Chinese article unless the user asks for a heavier editorial treatment.
- Treat "no visual" as a valid recommendation, not a failure.

### 3. Classify each slot

Use one primary class per slot. Add a fallback only when it materially helps production.

Read `references/illustration-taxonomy.md` when the article has mixed signals or when you need a tighter mapping from section pattern to visual type.

#### A. Diagram-first
- Use for flows, timelines, system maps, decision trees, mind maps, comparison matrices, and framework summaries.
- Prefer when the content can be expressed as nodes, steps, stages, or relationships.
- This is the best class for visuals that another AI assistant can generate directly.

#### B. Generative illustration prompt
- Use for abstract, atmospheric, or supportive visuals that set tone or reduce reading fatigue.
- Prefer when the section communicates a feeling, metaphor, or broad theme rather than evidence.
- Return a prompt the author can paste into Banana Pro, Gemini, Midjourney, or similar tools.

#### C. Author-captured evidence
- Use for product UIs, real conversations, terminal output, dashboards, settings pages, code review screens, or personal artifacts.
- Prefer when authenticity matters and AI-generated images would weaken credibility.
- Return actionable capture guidance instead of pretending the assistant can produce the image.

#### D. Data or reference visualization
- Use for metrics, rankings, proportions, before/after summaries, checklists, and pull-quote cards.
- Prefer simple charts, stat blocks, annotated tables, or quote cards over decorative art.
- This class is a useful addition beyond diagram / prompt / screenshot because many articles need information design, not scene generation.

#### E. Screenshot enhancement
- Use when a screenshot is necessary but the key takeaway is not visually obvious yet.
- Prefer callouts, numbered steps, crop guidance, comparison layouts, arrows, or magnified insets.
- Return annotation guidance, not image-generation prompts.

#### F. Cover image
- Use for the article hero image, Juejin cover, social card, or theme-setting opener.
- Treat this separately from body illustrations because its job is discovery and tone, not explanation.
- Prefer a short art-direction brief or prompt with headline-safe composition guidance.

#### G. No illustration needed
- Use when a section is already concrete, short, or repetitive.
- Explicitly say no image is recommended if adding one would dilute focus.

### 4. Make production-aware recommendations

- Optimize for the cheapest credible visual, not the fanciest one.
- Prefer diagrams over abstract artwork when the article explains structure.
- Prefer screenshots over generated images when the article claims real product experience.
- Recommend redaction, annotation, and crop guidance for manual captures.
- Flag risky ideas: copyrighted logos, fake dashboards, unreadable dense diagrams, or visuals that require information the author does not have.

## Output format

Always return four sections in this order.

### 1. Visual strategy summary

- Summarize the article's visual needs in 3-5 bullets.
- State the recommended visual density.
- Mention any constraints you inferred.

### 2. Visual plan table

Use a compact table with these columns:

- `slot`
- `section`
- `goal`
- `reader_job`
- `visual_class`
- `production_mode`
- `author_action`
- `priority`
- `why_here`
- `production_path`
- `optional`

### 3. Detailed briefs

For each recommended slot, include a brief based on its class:

- `Diagram-first`: diagram type, required nodes or stages, suggested labels, optional Mermaid starter.
- `Generative illustration prompt`: prompt, optional negative prompt, style notes, aspect ratio, text-avoidance guidance.
- `Author-captured evidence`: what to capture, where to navigate, exact page or state, crop focus, annotation ideas, redaction checklist.
- `Data or reference visualization`: chart/card type, exact data points, labels, ordering, caption suggestion.
- `Screenshot enhancement`: annotation plan, crop plan, comparison layout, and what should be visually emphasized.
- `Cover image`: title mood, topic metaphor, composition direction, and platform-fit notes.

Read `references/prompt-patterns.md` when you need prompt wording patterns or screenshot brief templates.

### 4. Editorial notes

- Call out any visuals to skip.
- Mention sequencing advice if the article should alternate dense and light sections.
- Mention platform-specific advice when relevant, such as keeping Juejin visuals clean and immediately readable on a narrow article column.

## Guardrails

- Do not recommend visuals purely for decoration.
- Do not fabricate screenshots or claim the assistant can capture private or unavailable interfaces.
- Do not recommend more manual screenshot work than the article can justify.
- Prefer legible, low-ink diagrams over overloaded diagrams.
- Do not behave like an image generation skill unless the user explicitly asks for prompts after planning.
- If article structure is weak, say so and suggest improving the outline before investing in illustration.

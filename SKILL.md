---
name: article-visual-planning
description: Analyze an article, blog post, newsletter draft, or long-form outline and make editorial illustration decisions before any image is produced. Trigger when the user asks to analyze article visuals, recommend article illustrations, generate article visual suggestions, plan blog post images, or in Chinese asks for 分析文章配图、推荐文章配图、生成文章配图、配图建议、文章插图建议、题图建议. Use when Codex needs to judge whether a section should have a visual at all, what job that visual should do, which visual class fits best, whether it should be a diagram, chart, abstract support image, real screenshot, screenshot enhancement, or cover image, and whether the author must create it manually. This skill is primarily for visual planning and decision support, not for directly generating final images, though it may provide prompts or briefs when helpful.
---

# Article Visual Planning

Turn article structure into a practical visual decision plan. Focus on reader comprehension, production feasibility, and platform fit instead of suggesting decorative images everywhere.

If the article already contains visual placeholders or constraints, honor them first. Otherwise, infer the minimum set of visuals that will materially improve understanding.

Treat this skill as an editorial advisor:

- first decide whether a visual is needed
- then decide what kind of visual would help
- then decide who should make it and how
- only then provide prompts or production guidance
- default to a text plan, not generated image files

## Language rule

- Reply in the user's language by default.
- If the user writes in Chinese, keep the full output in Chinese, including section headings and recommendation labels.
- If the user writes in English, keep the full output in English.
- Do not mix English field labels into a Chinese recommendation unless the user explicitly asks for bilingual output.

## Execution mode

### Trigger cues

- This skill should trigger for short, natural requests such as:
  - "帮我分析文章配图"
  - "给这篇文章做配图建议"
  - "生成文章配图"
  - "看看这篇文怎么配图"
  - "给这篇博客做题图和正文配图建议"
- Treat these requests as planning requests by default, not asset-generation requests.
- The presence of the verb "生成" does not override the text-first default unless the user explicitly names the output artifact, such as `svg`, `png`, Mermaid, cover image file, or rendered diagram.

### Default mode: text-first planning

- By default, this skill should return a fast Markdown recommendation, not final visual assets.
- Short requests like "分析文章配图", "生成文章配图", or "配图建议" should still stay in this mode.
- If the user asks to "generate", "save", or "put the result into a directory", interpret that as saving a text planning document unless they explicitly ask for image files.
- When file output is requested but the asset type is not specified, write one Markdown plan file such as `visual-plan.md`, `image-plan.md`, or another clearly named planning note near the article.
- If the article path is clear, prefer the output filename `visual-plan.md` in the same directory as the article.
- Keep the first pass lightweight and unblock the user quickly.

### Asset mode: explicit and separate

- Only generate actual assets when the user explicitly asks for them, for example: `svg`, `png`, `cover image`, `Mermaid diagram`, `draw this`, `export`, or `render`.
- Prefer a two-step flow when possible: first planning, then asset generation.
- If the user asks for both planning and final assets in one sentence, still finish the planning decision first and keep generated assets minimal.
- Never let SVG, Mermaid, or other long asset markup dominate the planning step.

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
- Keep recommendations short and editorial. Do not over-explain obvious tradeoffs.
- If the user wants the result written to disk, prefer writing a short Markdown plan over writing image assets.

## Output format

Always return concise Markdown sections in this order. Do not use tables unless the user explicitly asks for one.

The output must be scannable at first glance:

- each recommended visual gets its own heading
- the production method must be explicit near the top of each block
- the reader should know immediately whether this is author work, AI diagram work, AI image prompting, or screenshot enhancement
- keep the execution hint inside the same block whenever possible so the user does not need to jump between sections

### 1. Verdict first

- Start with 2-4 short bullets only.
- Lead with the main conclusion first, for example:
  - "Recommend 4 images total."
  - "Prioritize author screenshots and one AI diagram."
- Mention what to skip before listing what to make.
- Keep this section punchy and editorial, not analytical.

### 2. Recommended visuals

List only the visuals that are actually worth making.

Start with one short sentence:

`Suggested image count: X.`

Then list each recommendation as a self-contained block.

Use this exact shape:

```md
## Image 1 Title

Put it at: [section / paragraph / sentence anchor]
Priority: [must / recommended / optional]
Production method: [author screenshot / author screenshot + annotation / AI-generated diagram / AI image prompt / no image]
Recommended visual: [what the image should show]
Why: [one sentence]
Execution: [the most direct way to make it]
Prompt or brief: [only when execution would be easier with one]
```

If replying in Chinese, localize the shape like this:

```md
## 图1 标题

放在：[章节 / 段落 / 句子锚点]
优先级：[必做 / 推荐 / 可选]
生产方式：[作者手动截图 / 作者截图+轻标注 / AI 直接生成结构图 / AI 生图提示词 / 不建议配图]
推荐图：[这张图具体要表现什么]
为什么：[一句话]
怎么做：[最直接的制作方式]
提示词或 brief：[只有真的能帮用户直接执行时才写]
```

Rules:

- Default to 3-6 slots total.
- Omit low-value extras unless the user asks for more coverage.
- If a section should not get a visual, do not create a slot for it.
- Always surface `生产方式 / Production method` before the long explanation.
- Prefer headings such as `图1 标题图`, `图2 决策分流图`, `图3 6+1 分类图` over generic `配图建议 1`.
- Keep each block compact, but do not hide the execution decision.
- Give the decision first; do not walk through alternatives unless there is a real tradeoff.

### 3. Shared production notes (optional)

Only include this section when multiple visuals share the same constraint or when the prompts would become repetitive.

Examples:

- one shared note about article width, safe text size, or color direction
- one shared reminder about redaction or annotation style
- one shared prompt rule for all generative illustrations

If replying in Chinese, localize section titles too:

- `Verdict first` -> `结论先说`
- `Recommended visuals` -> `推荐配图`
- `Shared production notes (optional)` -> `统一制作说明（按需使用）`
- `Optional tradeoff note` -> `可选取舍`

Read `references/prompt-patterns.md` when you need prompt wording patterns or screenshot brief templates.

### 4. Optional file delivery note

- Add this section only when the user asked to save or write the result into the article directory.
- Keep it to 1-3 bullets.
- Say exactly what text file should be created, for example `visual-plan.md`.
- Do not use this section to announce generated SVG or PNG files unless the user explicitly asked for those formats.

### 5. Optional tradeoff note

- Add this section only if there is a real choice to make.
- Keep it to 1-2 bullets.
- Use it for "if you only make 3 images, keep these" or "if you skip one, skip this one".

## Guardrails

- Do not recommend visuals purely for decoration.
- Do not fabricate screenshots or claim the assistant can capture private or unavailable interfaces.
- Do not recommend more manual screenshot work than the article can justify.
- Prefer legible, low-ink diagrams over overloaded diagrams.
- Do not behave like an image generation skill unless the user explicitly asks for prompts after planning.
- Do not create `.svg`, `.png`, `.jpg`, `.webp`, `.drawio`, or other image assets during the default planning step.
- Do not generate long Mermaid or SVG blocks unless the user explicitly asks for a diagram artifact.
- If the user says "generate into this directory" but does not name an image format, create a Markdown plan file instead of visual assets.
- Treat "recommend and generate" as "generate the recommendation output" unless the user clearly requests final images.
- Keep planning fast; avoid long-running asset generation that blocks the recommendation itself.
- If article structure is weak, say so and suggest improving the outline before investing in illustration.
- Avoid repetitive compare/contrast commentary. Give the decision, then the reason, then move on.
- Prefer "what to make" over "all possible options".
- Prefer natural language recommendations over rigid schemas when readability matters.

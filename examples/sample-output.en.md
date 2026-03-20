# Sample Output (EN)

## Verdict first

- Recommend 5 images total. That is enough for this article.
- Prioritize credibility over decoration: the most important sections should use real screenshots.
- Skip visuals for the intro and conclusion.
- The strongest body visuals are the execution table and the `SKILL.md` screenshot; treat the cover separately.
- Default to a text visual plan first, not SVG or image files.

## Recommended visuals

Suggested image count: 5.

## Image 1 Intermediate failure-state screenshot

Put it at: right after the section where the problem becomes concrete.
Priority: recommended
Production method: author screenshot
Recommended visual: one early planning result that still feels noisy or unfocused.
Why: readers should see that the skill came from a real failure mode, not from abstract theorizing.
Execution: pick one existing draft screenshot, crop lightly, and keep the "too many ideas, not enough decision" feeling.

## Image 2 Execution table screenshot

Put it at: the start of the section where you explain the real run.
Priority: must
Production method: author screenshot
Recommended visual: a clean screenshot of the execution table showing slot, goal, type, production method, and priority.
Why: this is the strongest proof image in the article.
Execution: use a wide screenshot and keep the text readable; trim the table if it is too long.

## Image 3 `SKILL.md` screenshot

Put it at: the paragraph where you explain writing `SKILL.md`.
Priority: must
Production method: author screenshot + light annotation
Recommended visual: the `name`, `description`, and opening workflow lines from the skill file.
Why: this proves the method became a reusable skill.
Execution: capture only the key area and lightly highlight the "decide first, then recommend" part.

## Image 4 Brief comparison screenshot

Put it at: the cover-image section, before the final cover.
Priority: recommended
Production method: author screenshot + light annotation
Recommended visual: a before/after comparison that shows the brief became clearer.
Why: the improvement story is about better art direction, not just a different model.
Execution: place the two states side by side and lightly mark the fields that changed.

## Image 5 Final cover image

Put it at: the end of the cover-image section.
Priority: recommended
Production method: AI image prompt
Recommended visual: a restrained tech-article cover based on an AI teammate desk or an organized engineering workflow.
Why: the article needs one visible final result to close the loop.
Execution: place the finished cover image directly and keep the caption short.
Prompt or brief: practical lessons from three official Codex guides, for engineers and technical creators; show an AI teammate desk or an organized engineering workflow; mood capable, clear, modern, not overly sci-fi; leave safe space for title text; calm blue and neutral tones; avoid robots, neon cyberpunk, fake dense code, and cluttered collage.

## Shared production notes (optional)

- Keep screenshots real and clean; annotate only when the focal point is not obvious.
- Favor readability over decoration, especially in narrow blog layouts.

## File delivery note (optional)

- If the user only says "analyze article visuals" or "generate article visual suggestions", still return a text plan by default.
- If the user only says "generate into the article directory", write a text plan file such as `visual-plan.md` first.
- Only generate `svg`, `png`, Mermaid, or other visual artifacts when the requested asset type is explicit.

## Optional tradeoff note

- If only three visuals can be produced, keep: the execution table, the `SKILL.md` screenshot, and the final cover image.
- If one image must be cut, cut the intermediate planning screenshot first.

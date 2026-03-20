# article-visual-planning

这个仓库用于沉淀一个 Codex skill：先判断文章该不该配图、为什么配、配哪类图、谁来做，再给出最省力的视觉建议，而不是机械地“每段都配一张图”。

它本质上是一个“文章视觉编排建议 / 配图决策辅助” skill，不是一个单纯的“帮你生成图片”的 skill。

它主要回答这些问题：

- 这一段到底要不要配图
- 这张图承担什么作用
- 应该用哪一类视觉形式
- 该由 AI 直接生成、外部生图工具生成，还是作者自己截图
- 哪些图可以省略，避免打断阅读

它会顺带给出这些产出：

- 可直接生成的结构图：流程图、时间线、思维导图、对比矩阵
- 数据图表或信息卡片：柱状图、引用卡片、对比表、清单卡片
- 需要外部生图工具的提示词：用于抽象、氛围、辅助阅读类插图
- 需要作者亲自拍摄或截图的素材建议：用于真实界面、操作过程、证据型内容
- 截图增强建议：箭头、框选、局部放大、前后对比拼图
- 封面题图建议：用于掘金头图、博客头图、社交传播封面

## 当前结构

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

## 这个 skill 的核心判断

- 不是每段都要图
- 有结构关系，用图解
- 有数字、排名、对比，用信息型视觉
- 有抽象概念，用生图提示词
- 有真实界面或证据，用截图建议
- 截图不够清楚时，再给增强建议
- 题图单独判断，不和正文图混在一起
- 不需要图时，明确建议“不配图”

Skill 本体在 `/skill/article-visual-planning`。

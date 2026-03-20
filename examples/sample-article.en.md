# Sample Article (EN)

Title: I Read Three Official OpenAI Codex Guides and Turned Them Into One Practical Post

Platform: Juejin / blog
Audience: engineers and technical creators who are new to Codex
Goal: explain the main ideas clearly and help readers decide how to use Codex in real work

## Outline

### Intro

OpenAI published three official Codex guides. I read all of them and condensed the key ideas into one practical article. The main takeaway is simple: treat Codex as a configurable teammate, not a one-off tool.

### Part 1 - Eight practical habits

The first part explains how to use Codex better:

- write clearer prompts
- use plan mode for complex tasks
- store team rules in `AGENTS.md`
- let Codex run tests and review its own work
- connect external tools with MCP
- turn repeated workflows into Skills

One section explains Plan mode. Many readers have never seen it before, so a real screenshot would likely work better than plain text.

Another section introduces `AGENTS.md`. This is a core concept in the article because it explains how reusable rules are stored across projects and folders.

### Part 2 - Skills, Shell, and Compaction

This part explains three ideas together:

- Skills store repeatable workflows
- Shell gives Codex a real execution environment
- Compaction prevents long-running work from failing because the context gets too large

This section is about relationships between concepts rather than a single interface.

### Part 3 - AI across the software lifecycle

This part walks through planning, design, build, testing, code review, documentation, and operations.

The code review section mentions that Codex can review every PR and catch issues such as race conditions or risky hard-coded logic. A real screenshot of a review comment would make this claim more believable.

The operations section explains MCP-based log analysis. This is abstract, so readers may need help visualizing what “ask one prompt and trace logs + code + git history together” actually looks like.

### Conclusion

The closing message is that agents should handle the first pass, while engineers keep review, judgment, and risk control.

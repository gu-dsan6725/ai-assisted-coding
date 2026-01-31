# Part 2: AI-Assisted Coding with Google Antigravity

## Overview

In this section you will use [Google Antigravity](https://developers.googleblog.com/build-with-google-antigravity-our-new-agentic-development-platform/) to build the same data analytics and machine learning pipeline from Part 1. You will learn to configure Antigravity's customization features: **GEMINI.md/rules** for project instructions, **workflows** for on-demand commands, **skills** for reusable capabilities, and the **Manager view** for multi-agent orchestration.

## Key Concepts

### Rules (GEMINI.md + .agent/rules/)

Rules are always-on instructions that guide the agent's behavior. They function as system
instructions the agent considers before generating any code or plan.

- **Global rules**: `~/.gemini/GEMINI.md` -- applies to every project
- **Project rules**: `.agent/rules/*.md` -- applies to this project only

Rules are the equivalent of Claude Code's **CLAUDE.md**. Both provide persistent project
instructions, but Antigravity splits them into separate files per concern (one rule file
for coding style, another for data quality, etc.).

Reference: [Customize Antigravity with rules and workflows](https://atamel.dev/posts/2025/11-25_customize_antigravity_rules_workflows/)

### Workflows (.agent/workflows/)

Workflows are saved prompts triggered on demand with `/workflow-name`. They define
step-by-step instructions the agent follows when invoked.

Workflows are the equivalent of Claude Code's **slash commands** (`.claude/commands/`).
Both let you create reusable, explicitly triggered actions.

This project includes:
- `/run-eda`: Performs exploratory data analysis
- `/train-model`: Trains and evaluates an XGBoost model

### Skills (.agent/skills/)

Skills are directory-based packages containing a `SKILL.md` definition and optional
supporting files. The agent loads skills on demand when it determines they are relevant
to the current task.

Skills in Antigravity work similarly to Claude Code skills. Both:
- Are triggered automatically based on the agent's assessment of relevance
- Use a `SKILL.md` file as the entry point
- Can include supporting files (templates, scripts, references)

The key difference is directory location:
- Antigravity: `.agent/skills/<name>/SKILL.md` or `~/.gemini/antigravity/skills/<name>/SKILL.md`
- Claude Code: `.claude/skills/<name>/SKILL.md` or `~/.claude/skills/<name>/SKILL.md`

Reference: [Custom Skills in Google Antigravity](https://medium.com/google-cloud/tutorial-getting-started-with-antigravity-skills-864041811e0d)

### Manager View (Multi-Agent Orchestration)

Antigravity's Manager view lets you spawn and orchestrate multiple agents working in
parallel across workspaces. Each agent operates autonomously and produces artifacts
(task lists, plans, screenshots, code) that you can review.

This is Antigravity's approach to the problem Claude Code solves with **subagents**.

| Feature | Claude Code Subagents | Antigravity Manager View |
|---|---|---|
| Spawning | Automatic via Task tool | Manual from Manager UI |
| Monitoring | Results returned to main context | Artifact review in Manager |
| Parallelism | Concurrent subagents | Concurrent agents across workspaces |
| Verification | Hook-based automation | Artifact review + execution policies |

Reference: [Google Developers Blog: Antigravity](https://developers.googleblog.com/build-with-google-antigravity-our-new-agentic-development-platform/)

### Hooks Gap

Google Antigravity does **not** currently have native hook-based triggers equivalent to
Claude Code hooks. In Claude Code, hooks guarantee that commands (like ruff or py_compile)
run automatically at specific lifecycle points. In Antigravity, the closest alternatives are:

- **Rules**: Instruct the agent to always run quality checks (but not enforced programmatically)
- **Pre-commit framework**: Standard git hooks that run on commit
- **Workflow steps**: Include quality checks as explicit steps

Reference: [InfoWorld: A first look at Google's Antigravity IDE](https://www.infoworld.com/article/4096113/a-first-look-at-googles-new-antigravity-ide.html)

## The Workflow

1. **Plan**: Ask the agent to create an implementation plan (use "Auto" execution policy)
2. **Review**: Review the plan artifact, provide feedback
3. **Build**: Agent implements the plan following project rules
4. **Test**: Run quality checks manually or via pre-commit; review artifacts

## Getting Started

### Prerequisites
- Google Antigravity IDE installed ([Getting Started Codelab](https://codelabs.developers.google.com/getting-started-google-antigravity))
- Dependencies installed with `uv sync` (from the repo root)

### Run the Solved Examples

```bash
# From the repo root:
uv run python part2_antigravity/solved/01_eda.py
uv run python part2_antigravity/solved/02_feature_engineering.py
uv run python part2_antigravity/solved/03_xgboost_model.py
```

### Explore the Configuration

1. Read `.gemini/GEMINI.md` for global rules
2. Read `.agent/rules/code-style-guide.md` for project rules
3. Read `.agent/workflows/run-eda.md` and `.agent/workflows/train-model.md`
4. Read `.agent/skills/data-profiler/SKILL.md`

### Try the Workflows

Open Antigravity in this directory and try:
```
/run-eda
/train-model
```

## Solved Examples

| File | Description |
|------|-------------|
| `solved/01_eda.py` | Loads California Housing, computes statistics with polars, generates distribution and correlation plots |
| `solved/02_feature_engineering.py` | Creates derived features, handles infinite values, scales features, splits into train/test |
| `solved/03_xgboost_model.py` | Trains XGBoost regressor, computes metrics (RMSE, MAE, R2), generates residual and importance plots |

## Student Exercises

| Exercise | Topic | Key Skills |
|----------|-------|------------|
| [Exercise 1](exercises/exercise_1.md) | Rules and workflows | Create data quality rules, build an EDA workflow |
| [Exercise 2](exercises/exercise_2.md) | Custom skills | Build feature analysis and model comparison skills |
| [Exercise 3](exercises/exercise_3.md) | End-to-end with Manager view | Multi-agent orchestration, artifact review, hooks comparison |

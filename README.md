# AI-Assisted Coding Lab

In this lab you will use two AI-powered coding assistants -- **Claude Code** and **Google Antigravity** -- to build a complete data analytics and machine learning pipeline. The goal is to learn how these tools extend beyond simple code generation through features like hooks, skills, subagents, rules, and workflows.

## Learning Objectives

- Use an AI coding assistant to plan, build, and test a full ML project
- Configure **CLAUDE.md** and **GEMINI.md** to guide AI behavior with project-specific rules
- Create **hooks** that automate quality checks (linting, syntax validation) on every file change
- Build **custom skills** that teach the AI reusable workflows (data analysis, model evaluation)
- Use **subagents** to decompose complex tasks into isolated, parallel work streams
- Compare how Claude Code and Google Antigravity approach the same concepts differently

## Problem Statement

You are given the **California Housing** dataset (built into scikit-learn). Your task is to:

1. Perform exploratory data analysis (EDA) using polars and matplotlib
2. Engineer features and prepare the data for modeling
3. Train an **XGBoost** regression model to predict median house values
4. Evaluate the model and generate a performance report

You will complete this task twice -- once using Claude Code and once using Google Antigravity -- to understand how each tool's customization features support the development workflow.

## Prerequisites

- Python 3.11+
- [uv](https://docs.astral.sh/uv/) package manager installed
- Claude Code CLI installed (for Part 1)
- Google Antigravity IDE installed (for Part 2)

## Environment Setup

```bash
# Clone the repository
git clone <repo-url>
cd ai-assisted-coding

# Install uv (Python package manager)
curl -LsSf https://astral.sh/uv/install.sh | sh
source $HOME/.local/bin/env

# Install dependencies with uv
uv sync

# Verify the setup
uv run python -c "from sklearn.datasets import fetch_california_housing; print('Dataset OK')"
```

## Lab Structure

### Part 1: Claude Code

Located in `part1_claude_code/`. Focuses on:
- **CLAUDE.md**: Project-level instructions that guide Claude's behavior
- **Hooks**: Automated quality checks (ruff linting, py_compile) that run on every file write/edit
- **Skills**: Custom `/analyze-data` and `/evaluate-model` commands
- **Subagents**: Using Explore and Plan agents for task decomposition
- **Slash commands**: `/plan` for creating reviewable implementation plans

See [part1_claude_code/README.md](part1_claude_code/README.md) for detailed instructions.

### Part 2: Google Antigravity

Located in `part2_antigravity/`. Focuses on:
- **GEMINI.md + Rules**: Project rules that guide agent behavior
- **Workflows**: Saved prompts triggered with `/run-eda` and `/train-model`
- **Skills**: Custom data profiling capability
- **Manager View**: Multi-agent orchestration for parallel task execution

See [part2_antigravity/README.md](part2_antigravity/README.md) for detailed instructions.

## The AI-Assisted Development Workflow

Both parts follow the same development process:

1. **Plan**: Ask the AI assistant to create an implementation plan in a markdown file
2. **Review**: Read the plan, provide feedback, and request changes
3. **Build**: Have the AI execute the plan, writing code according to your project rules
4. **Test**: Hooks and automation catch issues automatically during development
5. **Iterate**: Review outputs, request improvements, and refine

This mirrors how professional developers work with AI coding assistants in practice.

## Concept Mapping

| Concept | Claude Code | Google Antigravity |
|---|---|---|
| Project instructions | `CLAUDE.md` | `GEMINI.md` + `.agent/rules/` |
| Reusable AI capabilities | Skills (`.claude/skills/`) | Skills (`.agent/skills/`) |
| On-demand commands | Slash commands (`.claude/commands/`) | Workflows (`.agent/workflows/`) |
| Automated checks | Hooks (PreToolUse, PostToolUse) | No native equivalent (use pre-commit) |
| Task decomposition | Subagents (Explore, Plan, Bash) | Manager View (multi-agent orchestration) |
| Execution control | Plan mode | Terminal execution policies (Off, Auto, Turbo) |

## Quick Reference

```bash
# Install dependencies
uv sync

# Run a solved example
uv run python part1_claude_code/solved/01_eda.py

# Lint all Python files
uv run ruff check .

# Format all Python files
uv run ruff format .

# Compile-check a file
uv run python -m py_compile part1_claude_code/solved/01_eda.py
```

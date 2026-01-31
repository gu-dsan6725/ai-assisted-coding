# Part 1: AI-Assisted Coding with Claude Code

## Overview

In this section you will use [Claude Code](https://code.claude.com/) to build a data analytics
and machine learning pipeline. You will learn to configure Claude Code's customization features:
**CLAUDE.md** for project rules, **hooks** for automated quality checks, **skills** for reusable
workflows, and **subagents** for task decomposition.

## Key Concepts

### CLAUDE.md

A markdown file that provides project-specific instructions to Claude. Claude reads this file
at the start of every session and follows its guidelines. Place it at the root of your project
or in nested directories for directory-specific rules.

The CLAUDE.md in this directory defines:
- Coding standards (type hints, logging format, function structure)
- Tool preferences (polars, uv, ruff)
- Output conventions

Reference: [Claude Code Memory](https://code.claude.com/docs/en/memory)

### Hooks

Hooks are shell commands or LLM prompts that execute automatically at specific points in
Claude Code's lifecycle. Unlike CLAUDE.md instructions (which are suggestions), hooks
**guarantee execution**.

This project configures two hooks in `.claude/settings.json`:

1. **PostToolUse (Write|Edit)**: After Claude writes or edits any file, `scripts/check_python.sh`
   runs `ruff check --fix` and `python -m py_compile` on Python files. If either fails, the error
   is reported back to Claude.

2. **PreToolUse (Bash)**: Before Claude runs any bash command, `scripts/block_force_push.sh`
   checks if the command is a `git push --force` and blocks it.

Hook types available:
- **Command** (`type: "command"`): Runs a shell script. Receives JSON on stdin, returns decisions via exit codes and stdout.
- **Prompt** (`type: "prompt"`): Sends a prompt to an LLM for single-turn yes/no evaluation.
- **Agent** (`type: "agent"`): Spawns a subagent with tool access (Read, Grep, Glob) for multi-turn verification.

Reference: [Claude Code Hooks](https://code.claude.com/docs/en/hooks)

### Skills

Skills are markdown files that teach Claude reusable workflows. They live in
`.claude/skills/<name>/SKILL.md` and can be invoked with `/skill-name` or loaded
automatically when Claude determines they are relevant.

This project includes two skills:
- `/analyze-data`: Performs exploratory data analysis on the California Housing dataset
- `/evaluate-model`: Evaluates a trained regression model and generates a performance report

Reference: [Claude Code Skills](https://code.claude.com/docs/en/skills)

### Slash Commands

Slash commands are markdown files in `.claude/commands/` that become available as `/command-name`.
This project includes:
- `/plan`: Creates a detailed implementation plan for review before building

Reference: [Claude Code Skills (includes slash commands)](https://code.claude.com/docs/en/skills)

### Subagents

Subagents are specialized Claude instances with isolated context windows. Claude spawns them
via the Task tool for specific subtasks:
- **Explore**: Read-only codebase exploration (Read, Grep, Glob)
- **Plan**: Design implementation approaches
- **Bash**: Execute shell commands
- **general-purpose**: Full tool access

Reference: [Claude Code Best Practices - Subagents](https://www.anthropic.com/engineering/claude-code-best-practices)

## The Workflow

1. **Plan**: Use `/plan` to have Claude create an implementation plan
2. **Review**: Read the plan in `.scratchpad/plan.md`, provide feedback
3. **Build**: Claude implements the plan; hooks run automatically on every file change
4. **Test**: Verify output, check that hooks caught issues, run the code

## Getting Started

### Prerequisites
- Claude Code CLI installed ([installation guide](https://code.claude.com/docs/en/quickstart))
- Dependencies installed with `uv sync` (from the repo root)

### Run the Solved Examples

```bash
# From the repo root:
uv run python part1_claude_code/solved/01_eda.py
uv run python part1_claude_code/solved/02_feature_engineering.py
uv run python part1_claude_code/solved/03_xgboost_model.py
```

This creates artifacts in the `output/` directory.

### Explore the Configuration

1. Read `CLAUDE.md` to see the project rules
2. Read `.claude/settings.json` to see the hook configuration
3. Read `.claude/skills/analyze-data/SKILL.md` and `.claude/skills/evaluate-model/SKILL.md`
4. Read `.claude/commands/plan.md`

### Try the Skills

Open Claude Code in this directory and try:
```
/analyze-data
/evaluate-model
/plan Add a feature importance analysis step
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
| [Exercise 1](exercises/exercise_1.md) | Create a custom `/generate-report` skill | Skill creation, SKILL.md frontmatter, supporting files |
| [Exercise 2](exercises/exercise_2.md) | Configure advanced hooks (command, prompt, agent) | Hook types, settings.json, exit codes, LLM evaluation |
| [Exercise 3](exercises/exercise_3.md) | End-to-end with subagents and plan mode | Plan-review-build workflow, Explore/Plan subagents |

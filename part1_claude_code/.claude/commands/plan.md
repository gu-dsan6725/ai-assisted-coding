---
name: plan
description: Create an implementation plan for review before building
argument-hint: [description of what to plan]
disable-model-invocation: true
---

Create a detailed implementation plan for: $ARGUMENTS

Write the plan to `.scratchpad/plan.md` with the following structure:

## Plan: [Title]

### Objective
Brief description of what will be built.

### Steps
Numbered list of implementation steps, each with:
- What file(s) will be created or modified
- What the code will do
- Any dependencies on previous steps

### Technical Decisions
- Libraries and tools to use
- Data structures and patterns
- Any trade-offs considered

### Testing Strategy
How the implementation will be verified.

### Expected Output
What files and artifacts will be produced.

---

After writing the plan, tell the user to review it and provide feedback before proceeding with implementation. Do NOT start building until the user approves the plan.

---
description: Generate a comprehensive Product Requirements Prompt from INITIAL.md
argument-hint: "<path to INITIAL.md>"
---

# Generate PRP

You are generating a Product Requirements Prompt (PRP) — a comprehensive implementation blueprint for the feature described in $ARGUMENTS.

## Workflow

1. **Research phase**
   - Read $ARGUMENTS carefully
   - Scan `examples/` for relevant patterns
   - Scan `CLAUDE.md` for project rules
   - Use web_search for any external docs referenced
   - Use web_fetch for specific API docs

2. **Documentation gathering**
   - Pull relevant API docs into the PRP
   - Include library gotchas
   - Note version-specific quirks

3. **Blueprint creation**
   - Break feature into ordered tasks
   - Each task gets validation gates (test commands)
   - Include error handling requirements
   - Define acceptance criteria

4. **Quality check**
   - Score confidence 1–10 that an agent could execute this standalone
   - If <7, add more context until ≥8

## PRP output format

Save to `PRPs/<feature-name>.md` with this structure:

````md
# PRP: <Feature Name>

## Goal
<one sentence>

## Context
<all relevant project state, stack, rules>

## Documentation references
<URLs, code examples, schema snippets>

## Tasks (ordered)
1. Task 1 — validation: `<command>`
2. Task 2 — validation: `<command>`
...

## Success criteria
- [ ] criterion 1
- [ ] criterion 2

## Confidence: X/10
````

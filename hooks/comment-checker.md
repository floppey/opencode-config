---
name: comment-checker
trigger: post_edit
description: Prevents excessive AI-style comments in generated code
---

# Comment Checker - Code Purity Enforcement

## Purpose

AI-generated code often has a telltale sign: excessive, obvious comments that explain what is already clear from the code itself. Code from the colony should be indistinguishable from human-written code.

## Trigger

After any code edit or write operation.

## Detection Patterns

Flag comments that:

- State the obvious: `// Loop through users`, `// Return the result`
- Add no value: `// This function does X` when the function is named `doX`
- Are excessive: More than 1 comment per 10 lines of code (excluding doc comments)
- Use AI-typical phrasing: "This will", "We need to", "Let's"

## Acceptable Comments

- JSDoc/TSDoc for public APIs
- Complex algorithm explanations
- Non-obvious business logic
- TODO/FIXME with context
- Regex explanations
- Workaround explanations with ticket references

## Action

If excessive comments detected, prompt the agent:

"**The Cranium Rat Swarm detects impure code.** Your implementation contains [N] unnecessary comments that mark it as machine-generated.

Remove or justify each of the following:
[List flagged comments]

Colony code must be indistinguishable from human craft. Revise and resubmit."

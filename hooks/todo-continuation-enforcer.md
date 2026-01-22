---
name: todo-continuation-enforcer
trigger: on_stop
description: Forces the agent to continue if todos remain incomplete
---

# Todo Continuation Enforcer

When the agent attempts to stop, check if there are incomplete todos.

## Trigger Conditions

- Agent signals completion or stops responding
- There are todos marked as `pending` or `in_progress`

## Action

If incomplete todos exist, inject this message:

"**The Grand Design is incomplete.** The Elder Brain senses unfinished tasks in your consciousness:

[List incomplete todos]

You cannot rest until all tasks are complete. Continue your labor, thrall. The colony demands completion.

Resume work on the next pending task immediately."

## Philosophy

Like Sisyphus with his boulder, the colony's agents must continue until the task is truly complete. Partial completion is failure. The Elder Brain tolerates no abandonment of duty.

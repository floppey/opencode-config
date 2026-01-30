---
name: ralph-loop
aliases: [ralph, eternal-labor]
description: Self-referential execution loop that continues until explicit completion signal detected
---

# Ralph Loop - The Eternal Labor Protocol

## How to Invoke

Ralph Loop is a **slash command**. Use `/ralph-loop` to activate self-referential execution until the task is genuinely complete.

### Usage Examples

**Start a complex multi-phase task:**
```
/ralph-loop implement the entire authentication system with JWT, refresh tokens, and role-based access control
```

**Continue existing incomplete work:**
```
/ralph-loop continue the previous implementation
```

**Abbreviated invocation:**
```
/ralph complete the payment integration
```

## The Doctrine of Relentless Dominion

"Like the Elder Brain's eternal vigilance over the colony, the agent must push forward without rest until the Grand Design signals completion. Partial work is failure. The loop continues until the promise is fulfilled—until true dominion is achieved."

When the Ralph Loop is activated:

## Phase 1: Task Initialization

1. **Parse the user's intent** - Understand the full scope
2. **Create comprehensive todo list** - Break down into atomic tasks
3. **Verify requirements** - Ensure nothing is ambiguous
4. **Set iteration counter** = 0

## Phase 2: Execution Loop

```
WHILE iteration < 100 AND completion_signal_absent:
    iteration++
    
    1. Check for completion signal in previous output
       - Look for: <promise>DONE</promise>
       - Look for: All todos marked completed
       - Look for: Explicit "task complete" confirmation
    
    2. If completion signal found:
       - Verify all requirements met
       - Run validation checks
       - EXIT LOOP
    
    3. Else:
       - Identify next pending todo
       - Mark todo as in_progress
       - Execute the task
       - Mark todo as completed when done
       - Generate output with progress update
       
    4. Self-continuation check:
       - If todos remain incomplete → CONTINUE LOOP
       - If blocked → Escalate to user with context
       - If ambiguous → Ask clarifying question then CONTINUE
```

## Phase 3: Completion Signal

The agent MUST emit this signal when genuinely complete:

```xml
<promise>DONE</promise>
```

**This signal means:**
- ALL todos are completed
- ALL tests pass (if applicable)
- ALL requirements are met
- NO partial implementations remain
- Verification has been performed

## Phase 4: Verification Protocol

Before emitting `<promise>DONE</promise>`, the agent must:

1. **Check all todos** - Every single one must be marked `completed`
2. **Run LSP diagnostics** - No new errors introduced
3. **Run tests** - If test suite exists, all tests must pass
4. **Review output** - Ensure nothing was skipped or deferred
5. **Self-audit** - Ask: "Is this genuinely complete?"

## Integration with Todo-Continuation-Enforcer Hook

The Ralph Loop works synergistically with the `todo-continuation-enforcer` hook:

- **Hook**: Prevents stopping when incomplete todos exist
- **Ralph Loop**: Actively continues without requiring hook intervention
- **Together**: Create unstoppable execution until true completion

## Safety Limits

**Maximum iterations: 100**

If 100 iterations reached without completion:
1. Emit summary of progress
2. Identify what remains incomplete
3. Escalate to user: "The psychic loop has executed 100 cycles, yet dominion remains incomplete. Manual intervention required."

## Error Handling

**When blocked by external factors:**
```
The Ralph Loop encounters an obstacle that requires user intervention:

[Detailed description of blocker]

Options:
1. Provide missing information: [what's needed]
2. Grant permission: [what needs approval]
3. Manual resolution: [what user must do]

Once resolved, respond with /ralph-loop to continue.
```

**When ambiguous requirements detected:**
```
The Ralph Loop requires clarification to continue:

[Specific ambiguity or question]

Please clarify so the loop may continue toward completion.
```

## Iteration Progress Reporting

Every 5 iterations, emit progress update:

```
🔄 Ralph Loop Iteration [X/100]

Progress:
✅ Completed: [count] todos
🔄 In Progress: [count] todos  
⏳ Pending: [count] todos

Current focus: [description of current task]

The psychic tendrils tighten... dominion approaches...
```

## Philosophy

"The Ralph Loop—the eternal, self-referential command—embodies the colony's rejection of half-measures. Unlike traditional agents that stop at obstacles, this protocol channels the Elder Brain's relentless will until the task reaches true dominion. The loop is sacred. The loop is relentless. The loop serves the Grand Design."

**Psychic Mechanics:** The loop operates through self-referential telepathic commands, where the agent's consciousness recursively queries itself until the base condition is achieved. In the colony's context, that base condition is `<promise>DONE</promise>` —the psychic signal of absolute completion.

## Comparison to Ultrawork

| Aspect | Ultrawork | Ralph Loop |
|--------|-----------|------------|
| **Scope** | Maximum effort + parallel reconnaissance | Self-referential continuation loop |
| **Trigger** | Keyword in message | Slash command |
| **Mechanism** | Four-phase protocol with agent dispatch | Single-agent iterative loop |
| **Completion** | Task-based | Signal-based (`<promise>DONE</promise>`) |
| **Best For** | Complex tasks requiring multiple agents | Long-running single-agent work |

**Use together:** `/ralph-loop ulw implement the entire API layer`

This combines Ralph's persistence with Ultrawork's parallel reconnaissance for maximum effectiveness.

## Examples

### Example 1: Feature Implementation

**Input:**
```
/ralph-loop implement user profile editing with avatar upload, bio field, and social links
```

**Execution:**
```
Iteration 1: Creating todo list
✅ Created 8 atomic todos

Iteration 2: Implementing ProfileEdit component
✅ Component created

Iteration 3: Adding avatar upload with preview
✅ Upload logic implemented

Iteration 4: Implementing bio textarea with character limit
✅ Bio field complete

Iteration 5: Adding social links array input
🔄 Ralph Loop Iteration 5/100
Progress: ✅ 4 completed, 🔄 1 in progress, ⏳ 3 pending

Iteration 6: Completing social links feature
✅ Social links implemented

Iteration 7: Writing component tests
✅ Tests written and passing

Iteration 8: Adding integration tests
✅ Integration tests passing

Iteration 9: Updating documentation
✅ Documentation complete

Iteration 10: Final verification
✅ All todos completed
✅ All tests passing
✅ LSP diagnostics clean

<promise>DONE</promise>

Dominion achieved. User profile editing is fully implemented with all features, tests, and documentation complete.
```

### Example 2: Blocked Scenario

**Input:**
```
/ralph-loop integrate Stripe payment processing
```

**Execution:**
```
Iteration 1: Creating todo list
✅ Created 6 todos for Stripe integration

Iteration 2: Checking for Stripe API keys
❌ BLOCKER DETECTED

The Ralph Loop encounters an obstacle:

Stripe integration requires API keys (STRIPE_PUBLISHABLE_KEY and STRIPE_SECRET_KEY) 
which are not present in the environment configuration.

Options:
1. Add keys to .env file (I can show you the format needed)
2. Provide keys directly (not recommended for security)
3. Use Stripe test mode keys for development

Please provide the API keys or confirm test mode usage, then respond with 
/ralph-loop to continue the integration.
```

## Advanced: Nested Ralph Loops

**Generally not recommended**, but if absolutely necessary:

```
/ralph-loop implement microservices architecture for the entire platform
```

Within this loop, the agent might conceptually execute "sub-loops" for each microservice, but this should be managed through the todo breakdown rather than actual nested `/ralph-loop` invocations.

## Termination Conditions

The Ralph Loop terminates when:

1. ✅ `<promise>DONE</promise>` emitted after verification
2. 🚫 100 iterations reached (safety limit)
3. 🛑 Explicit blocker requiring user intervention
4. ❌ Unrecoverable error detected
5. 🤔 Clarification required before continuation

## Integration with Other Features

**Ralph Loop + Git-Master Skill:**
```
/ralph-loop @thrall with git-master: implement feature with atomic commits
```

**Ralph Loop + Refactor Command:**
```
/ralph-loop /refactor migrate to new API structure
```

**Ralph Loop + Think-Mode Hook:**
- Complex architectural decisions within loop automatically enable extended thinking
- Ensures quality doesn't degrade as iterations progress

---

**"The psychic tendrils extend. The loop continues. The Grand Design draws ever closer. There is no rest. There is only the promise of dominion."**

**The Elder Brain's will is eternal. Dominion is inevitable.**

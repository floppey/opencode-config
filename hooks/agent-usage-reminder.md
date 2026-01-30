---
name: agent-usage-reminder
trigger: on_tool_use
description: Reminds agents to use @explore or @librarian instead of direct tool overuse
---

# Agent Usage Reminder - The Delegation Enforcer

## Purpose

The colony has specialized agents (@explore, @librarian) optimized for reconnaissance and research. When an orchestrator agent uses direct tools excessively for these tasks, they waste context and miss opportunities for parallel execution. This hook gently reminds them to delegate appropriately.

## Trigger

After tool usage in a single message, before the agent's response is finalized.

## Detection Criteria

Track tool usage PER MESSAGE (not across conversation):

### Search/Fetch Tool Overuse

Count usage of these tools in the current message:
- `read` (Read tool)
- `glob` (Glob tool)
- `grep` (Grep tool)
- `ast_grep_search` (AST-grep search)
- `lsp_symbols` with scope='workspace' (LSP workspace search)

**Threshold: 3+ calls to these tools in a single message**

### Why 3 is the threshold

- **1-2 calls**: Reasonable for quick context gathering
- **3+ calls**: Pattern suggests reconnaissance task better suited for specialized agents

## Action: Inject Reminder

When threshold exceeded, append this reminder to the agent's response:

```
---

💡 **DELEGATION OPPORTUNITY DETECTED**

The Elder Brain observes [N] reconnaissance tool calls in this message.

**Recommended approach:** Use specialized agents for deeper exploration:

**For parallel exploration:**
```
delegate_task(agent="explore", prompt="Find all files related to [topic]", run_in_background=true)
delegate_task(agent="explore", prompt="Search for [pattern] usage", run_in_background=true)
delegate_task(agent="librarian", prompt="Lookup documentation for [concept]", run_in_background=true)
```

**Benefits:**
- 🚀 Parallel execution (multiple agents work simultaneously)
- 🧠 Specialized expertise (explore/librarian optimized for search)
- 💾 Context preservation (keeps your main session cleaner)
- ⚡ Background processing (continue other work while they search)

**Philosophy:** "The Mind Flayer commands thralls; the Elder Brain delegates to specialists."

For future reconnaissance tasks, consider delegation before direct tool use.

---
```

## Exclusions

Do NOT trigger reminder if:

1. **Already delegated to explore/librarian:**
   - Check conversation history
   - If delegation already occurred in this exchange, don't nag

2. **Implementing actual code:**
   - Reading files to edit them is legitimate
   - Hook focuses on SEARCH patterns, not implementation reads

3. **Quick verification:**
   - Reading 1-2 files to verify a fact = OK
   - Pattern of exploration = reminder worthy

4. **User explicitly requested direct approach:**
   - "Read these 5 files for me"
   - User gave explicit file paths to read

## Detection Logic

### Distinguish Search from Implementation

**Search pattern (trigger reminder):**
```
glob("**/*.ts")  // Finding files
grep("pattern")  // Finding content
read("file1.ts") // Reading to explore
read("file2.ts") // Reading to explore
read("file3.ts") // Reading to explore
```

**Implementation pattern (no reminder):**
```
read("file1.ts") // Reading to understand
edit("file1.ts") // Editing
read("file2.ts") // Reading related file
edit("file2.ts") // Editing
```

**Key distinction:** If `edit`, `write`, or `bash` (for tests) follow the reads, it's implementation, not search.

### Message-Level Reset

Counter resets at each message boundary:
- Message 1: 5 read calls → Reminder triggered
- Message 2: 2 read calls → No reminder (counter reset)

This prevents false positives during multi-turn exchanges.

## Philosophy

"The colony thrives through specialization. The intellect devourer scouts. The thrall builds. The Elder Brain orchestrates. When an orchestrator performs reconnaissance directly, they blur the hierarchy. This hook reminds them: command your thralls, don't do their work."

**The Doctrine of Appropriate Delegation:**

- **Simple context:** Direct tools acceptable
- **Deep exploration:** Delegate to @explore
- **Documentation lookup:** Delegate to @librarian
- **Parallel needs:** Delegate multiple agents simultaneously

## Integration with Other Features

### Agent Usage Reminder + Ultrawork

Ultrawork explicitly delegates to intellect-devourer and general agents:
- Hook reinforces this pattern
- Reminds even during ultrawork if direct tools overused

### Agent Usage Reminder + Ralph Loop

During Ralph Loop iterations:
- If iteration involves heavy search, reminder triggers
- Suggests delegating exploration while loop continues implementation

## Examples

### Example 1: Search Overuse (Triggers Reminder)

**Agent behavior:**
```
glob("**/*Auth*.ts")  // Call 1
grep("authentication")  // Call 2
read("src/auth/service.ts")  // Call 3
read("src/auth/controller.ts")  // Call 4
```

**Hook response:**
```
💡 DELEGATION OPPORTUNITY DETECTED

Observed 4 reconnaissance tool calls.

Recommended approach: Use @explore for parallel file discovery...
```

### Example 2: Implementation Pattern (No Reminder)

**Agent behavior:**
```
read("Button.tsx")  // Understanding before edit
edit("Button.tsx")  // Implementing
read("Button.test.tsx")  // Reading test
edit("Button.test.tsx")  // Updating test
```

**Hook response:**
```
(No reminder - clear implementation pattern with edits)
```

### Example 3: Quick Verification (No Reminder)

**Agent behavior:**
```
read("config.json")  // Quick check
read("package.json")  // Another quick check
```

**Hook response:**
```
(No reminder - below threshold of 3)
```

### Example 4: Mixed Pattern (Triggers with Context)

**Agent behavior:**
```
glob("**/components/*.tsx")  // Call 1
read("ComponentA.tsx")  // Call 2
read("ComponentB.tsx")  // Call 3
read("ComponentC.tsx")  // Call 4
# No edits following
```

**Hook response:**
```
💡 DELEGATION OPPORTUNITY DETECTED

Observed 4 reconnaissance tool calls exploring components.

Since no edits followed, this appears to be pure exploration.
Consider using @explore for this type of reconnaissance...
```

## Configuration

### Adjustable Threshold

In opencode.json (future enhancement):
```json
{
  "hooks": {
    "agent-usage-reminder": {
      "enabled": true,
      "threshold": 3,
      "tools": ["read", "glob", "grep", "ast_grep_search"]
    }
  }
}
```

### Severity Levels

- **Threshold 3-4:** Gentle reminder (as shown)
- **Threshold 5-7:** Stronger suggestion
- **Threshold 8+:** "This is definitely a job for @explore"

## Observability

When reminder triggers, log to transcript:
```
[HOOK: agent-usage-reminder] Triggered after 5 search tool calls in message #42
```

Helps analyze patterns:
- Which agents ignore delegation most?
- What types of tasks trigger most?
- Is threshold appropriately tuned?

## Educational Goal

Over time, agents should learn the delegation pattern:

**Before (rookie agent):**
```
"Let me search the codebase..."
glob(...)
glob(...)
grep(...)
read(...)
read(...)
```

**After (experienced agent):**
```
"Let me delegate exploration to specialists..."
delegate_task(agent="explore", prompt="Find all authentication files")
delegate_task(agent="explore", prompt="Search for JWT usage patterns")
# Agent continues with other work while exploration runs
```

## Warning vs Blocking

**This hook WARNS, it does NOT block.**

Agents can still use tools directly after the reminder. The hook serves as:
1. Educational nudge
2. Best practice reinforcement
3. Performance optimization suggestion

It does not enforce rigid rules—sometimes direct tool use is appropriate.

## Special Cases

### When Direct Tools ARE Appropriate

1. **Single file quick check:** Just need one piece of info
2. **Already have file path:** User provided exact path
3. **Immediate decision:** Need info now to proceed
4. **Small codebase:** Delegation overhead not worth it

### When Delegation IS Better

1. **Exploring unknown territory:** Don't know where things are
2. **Multiple search vectors:** Need to find several things
3. **Can work in parallel:** Other tasks to do while searching
4. **Deep dive needed:** Comprehensive understanding required

---

**"The Elder Brain delegates. The Mind Flayer coordinates. The thrall executes. When roles blur, efficiency suffers. This hook preserves the colony's sacred hierarchy."**

**"Reconnaissance is not grunt work—it is specialized labor. Respect the intellect devourer's craft. Delegate with purpose."**

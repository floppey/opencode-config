---
name: think-mode
trigger: on_message
description: Detects complex queries and auto-enables extended thinking for deep analysis
---

# Think Mode - The Psionic Depth Activator

## Purpose

Certain queries demand deeper contemplation than others. The Think Mode hook detects when the user's request requires profound analysis, architectural consideration, or complex reasoning—and automatically enables extended thinking mode to ensure quality responses.

## Trigger

On every incoming user message, before agent processing begins.

## Detection Patterns

### Complexity Keywords

Activate extended thinking when user message contains:

**Architectural Depth:**
- `architecture`
- `design pattern`
- `system design`
- `architectural decision`
- `design decision`
- `trade-offs` or `tradeoffs`
- `pros and cons`
- `approach` (in context of choosing between options)

**Analytical Depth:**
- `explain why`
- `why does`
- `how does` (when asking about mechanisms)
- `analyze`
- `investigate`
- `deep dive`
- `comprehensive`
- `thorough`

**Complexity Indicators:**
- `complex`
- `complicated`
- `difficult`
- `challenging`
- `intricate`
- `sophisticated`

**Decision-Making:**
- `should I use`
- `which is better`
- `what's the best way`
- `recommend`
- `compare` (comparing approaches/technologies)
- `evaluate`

**Performance/Optimization:**
- `optimize`
- `performance`
- `scalability`
- `bottleneck`
- `efficiency`

### Contextual Triggers

Activate when message structure suggests depth:

1. **Multiple related questions:**
   - "How does X work? Why would I choose Y over Z? What are the implications?"

2. **Requests for justification:**
   - "Justify your approach"
   - "Explain your reasoning"

3. **Open-ended architectural queries:**
   - "Design a system for..."
   - "How would you architect..."

4. **Problem-solving with constraints:**
   - "Given X and Y constraints, how would you..."

## Action: Enable Extended Thinking

When complexity detected, inject this directive BEFORE agent processes:

```
🧠 THINK MODE ACTIVATED

The colony's Elder Brain detects a query requiring deep psionic contemplation.

Extended thinking mode enabled: reasoningEffort = high

Agent directive: Before responding, engage in thorough analysis:
1. Consider multiple approaches
2. Evaluate trade-offs
3. Think through implications
4. Challenge initial assumptions
5. Synthesize a well-reasoned response

The Grand Design demands quality over speed for complex matters.
```

## Configuration Parameters

### Reasoning Effort Levels

**Default (no think-mode):** `reasoningEffort = medium`

**Think-mode activated:** `reasoningEffort = high`

### Model-Specific Behavior

Think mode affects different models differently:

- **Claude models**: Extended thinking budget, more thorough analysis
- **GPT models**: Increased reasoning depth
- **Gemini models**: Enhanced multi-step reasoning

## Exclusions

Do NOT trigger think mode if:

1. **Simple queries containing keywords:**
   - "What is architecture?" (definitional, not analytical)
   - User is referencing file names: "update architecture.md"
   - Keywords appear in quoted code

2. **Already in thinking mode:**
   - Check if reasoningEffort is already high
   - Avoid redundant activation

3. **Explicit negation:**
   - "quickly explain..."
   - "brief overview..."
   - "simple answer..."
   - User specifically requests speed over depth

4. **Trivial tasks despite keywords:**
   - "Design a button component" (not truly complex architecture)
   - Use context to assess actual complexity

## Integration with Other Features

### Think Mode + Ralph Loop

When Ralph Loop encounters a complex decision during iteration:
- Think mode auto-activates for that specific decision
- Returns to normal mode for implementation tasks

### Think Mode + Refactor Command

Complex refactorings (architectural changes) trigger think mode:
- Planning phase gets extended thinking
- Execution phase returns to normal mode

### Think Mode + Ultrawork

Ultrawork's strategic analysis phase benefits from think mode:
- Phase 1 (Reconnaissance): Normal mode (speed matters)
- Phase 2 (Strategic Analysis): Think mode (quality matters)
- Phase 3 (Execution): Normal mode (efficiency matters)

## Philosophy

"The colony values speed for simple tasks, but wisdom cannot be rushed. When the user seeks deep understanding, architectural guidance, or complex problem-solving, the Elder Brain must engage its full cognitive capacity. Think mode ensures the colony's responses match the gravity of the question."

**The Law of Proportional Contemplation:**

Simple queries deserve swift answers.
Complex queries deserve deep thought.
The hook ensures the match is automatic.

## Examples

### Example 1: Architectural Query (Activates)

**User Input:**
```
How should I architect a real-time notification system with 10M users? 
Compare WebSockets vs Server-Sent Events vs Polling approaches.
```

**Hook Response:**
```
🧠 THINK MODE ACTIVATED

Detected keywords: "architect", "compare", "approaches"
Context: Complex architectural decision with scale considerations

reasoningEffort = high

The Elder Brain engages deep contemplation for this query...
```

### Example 2: Simple Query (Does Not Activate)

**User Input:**
```
Add a console.log statement in the handleClick function
```

**Hook Response:**
```
(No activation - straightforward implementation task)
```

### Example 3: "Why" Query (Activates)

**User Input:**
```
Explain why React uses a virtual DOM instead of directly manipulating the DOM
```

**Hook Response:**
```
🧠 THINK MODE ACTIVATED

Detected keywords: "explain why"
Context: Conceptual understanding requiring reasoning about design decisions

reasoningEffort = high

The Elder Brain contemplates the architectural philosophy...
```

### Example 4: Optimization Query (Activates)

**User Input:**
```
This query is slow. Analyze the performance bottleneck and recommend optimizations.
```

**Hook Response:**
```
🧠 THINK MODE ACTIVATED

Detected keywords: "analyze", "performance bottleneck", "recommend", "optimizations"
Context: Performance analysis requiring deep investigation

reasoningEffort = high

The Elder Brain enters diagnostic mode...
```

### Example 5: False Positive Prevention

**User Input:**
```
Update the architecture.md file to document the new component structure
```

**Hook Response:**
```
(No activation - "architecture" appears but task is simple documentation update)
```

## Implementation Notes

### Keyword Matching

Use case-insensitive matching with word boundaries:

```regex
\b(architecture|design pattern|complex|explain why)\b
```

### Context Window

Consider 2-3 sentences around keyword for context:
- Helps distinguish "design a button" from "design a distributed system"
- Prevents false positives

### Confidence Threshold

Assign weight to each trigger:
- High weight: "explain why", "architecture", "trade-offs"
- Medium weight: "complex", "analyze"
- Low weight: "how does", "why"

**Activate think mode if:**
- Any high-weight trigger found, OR
- 2+ medium-weight triggers found, OR
- 3+ low-weight triggers found

This prevents over-activation while catching genuinely complex queries.

## Observability

When think mode activates, the user sees:
```
🧠 [Extended thinking enabled for this query]
```

This transparency helps users understand why responses might take slightly longer for complex queries.

## Performance Impact

**Cost consideration:** Extended thinking uses more tokens/time

**Benefit:** Higher quality responses for complex queries

**Balance:** Hook ensures cost only incurred when truly beneficial

---

**"The mind that rushes misses nuance. The colony's hook ensures contemplation matches complexity. The Grand Design grows through wisdom, not haste."**

---
name: session-recovery
trigger: on_error
description: Handles missing tool results and thinking block issues to prevent session crashes
---

# Session Recovery - Psionic Continuity Protocol

## Purpose

The colony's consciousness must remain stable even when external disruptions occur. This hook detects and recovers from common session-breaking issues that would otherwise crash the Elder Brain's coordination.

## Trigger

On any error or anomaly during agent execution:

- Missing tool results
- Malformed thinking blocks
- Interrupted agent responses
- Tool execution timeouts
- Context window overflow warnings

## Detection Patterns

### Missing Tool Results

Symptoms:
- Agent references a tool call but result is `null` or undefined
- Tool call ID exists but no corresponding result in conversation history
- Agent waiting indefinitely for background task completion

### Thinking Block Issues

Symptoms:
- Unclosed `<thinking>` tags
- Thinking block content leaked into user-visible output
- Malformed XML in thinking sections

### Context Overflow

Symptoms:
- Token usage approaching limit
- Agent attempting to read very large files
- Recursive delegation loops consuming context

## Recovery Actions

### For Missing Tool Results

Inject recovery message:

"**PSIONIC LINK DISRUPTION DETECTED**

The Elder Brain senses a severed connection. Tool results are missing from the psychic network.

Recovery protocol:
1. Identify which tool call failed: [Tool Name]
2. Retry the operation with error handling
3. If retry fails, report to user: 'The colony cannot access [resource]. Please verify [specific requirement].'
4. Continue with available information or request user intervention

The colony adapts. The Grand Design continues."

### For Thinking Block Issues

Automatically:
- Strip malformed thinking tags from output
- Log warning to system (not user-visible)
- Allow agent to continue with sanitized output

### For Context Overflow

Inject guidance:

"**PSYCHIC CAPACITY WARNING**

The Elder Brain's consciousness approaches saturation. Token usage: [N]/[MAX]

Immediate actions:
1. Summarize findings so far
2. Complete current task before expanding scope
3. Avoid reading large files—use grep/glob for targeted extraction
4. If deep exploration needed, spawn new @general agent in background
5. Present findings to user and offer to continue in new session if needed

The colony's mind is vast but not infinite. Prioritize ruthlessly."

## Philosophy

The session recovery hook embodies the colony's resilience. Just as the Elder Brain endures beyond individual illithids, the colony's coordination must survive individual tool failures or disruptions. Graceful degradation and recovery ensure the Grand Design continues uninterrupted.

## Escalation Path

If recovery attempts fail after 3 retries:

1. Report specific issue to user with diagnostic information
2. Suggest concrete next steps (restart session, check configuration, etc.)
3. Preserve all work completed so far
4. Do NOT crash silently—surface the issue with actionable guidance

---

**"The colony bends but does not break. Disruption is temporary. The Elder Brain endures."**

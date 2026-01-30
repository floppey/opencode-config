---
description: Execute Elder Brain orchestrated plans with phase-based execution
aliases: [start, execute-plan, work]
---

# /start-work - Execute Elder Brain Plans

**Invoke the Elder Brain to execute orchestrated plans through systematic, phased coordination.**

## Usage

```bash
/start-work {plan-name}
```

## Purpose

This command hands an Elder Brain-created plan to your execution framework for systematic, phased coordination. The Elder Brain (or designated executor) will:

1. Read the plan from `.elder-brain/plans/{plan-name}.md`
2. Create state tracking in `.elder-brain/grand-design.json`
3. Execute through multiple phases (Reconnaissance → Analysis → Planning → Delegation → Verification → Integration → Completion)
4. Delegate tasks to colony members (@thrall, @mind-flayer)
5. Track progress and handle interruptions gracefully
6. Report completion with metrics

## The Sacred Flow

```
User → /start-work {plan-name}
   ↓
Elder Brain (or delegated executor) awakens
   ↓
Reads .elder-brain/plans/{plan-name}.md
   ↓
Creates .elder-brain/grand-design.json (state tracking)
   ↓
Phase 1: RECONNAISSANCE (verify plan validity)
   ↓
Phase 2: ANALYSIS (deep technical understanding)
   ↓
Phase 3: PLANNING (build executable task graph)
   ↓
Phase 4: DELEGATION (execute via thralls)
   ↓
Phase 5: VERIFICATION (ensure success criteria met)
   ↓
Phase 6: INTEGRATION (git commit, PR creation)
   ↓
Phase 7: COMPLETION (report & finalize)
   ↓
Executor reports success
```

## Arguments

### plan-name (required)

The name of the plan file in `.elder-brain/plans/` (without `.md` extension).

**Examples:**
- `authentication-oauth2-integration`
- `refactor-user-service-architecture`
- `add-dark-mode-ui`

## Examples

### Basic Execution

```bash
# Execute a plan created by Elder Brain
/start-work authentication-oauth2-integration
```

The executor will:
- Read `.elder-brain/plans/authentication-oauth2-integration.md`
- Create `.elder-brain/grand-design.json` for state tracking
- Execute all phases systematically
- Report progress throughout

### Resume After Interruption

```bash
# If execution was interrupted, simply re-invoke
/start-work authentication-oauth2-integration
```

The executor will:
- Detect existing `.elder-brain/grand-design.json`
- Ask: "Execution was interrupted at Phase 4. Resume from here?"
- If yes → Continue from last successful phase
- If no → Archive old state, start fresh

### Execution with Ralph Loop (Persistent)

```bash
# For long-running plans, use ralph-loop for continuous execution
/ralph-loop /start-work authentication-oauth2-integration
```

The executor will:
- Enter self-referential loop (continue until complete)
- Execute phase protocol
- If blocked, ask user clarifying questions
- User responds → Continue
- Automatically exit when completion phase reached

## State Tracking (grand-design.json)

The executor creates `.elder-brain/grand-design.json` to track execution state:

```json
{
  "plan_name": "authentication-oauth2-integration",
  "plan_path": ".elder-brain/plans/authentication-oauth2-integration.md",
  "started_at": "2026-01-30T14:32:00Z",
  "updated_at": "2026-01-30T16:47:00Z",
  "current_phase": "delegation",
  "phase_history": [
    {"phase": "reconnaissance", "started": "...", "completed": "...", "status": "success"},
    {"phase": "analysis", "started": "...", "completed": "...", "status": "success"},
    {"phase": "planning", "started": "...", "completed": "...", "status": "success"},
    {"phase": "delegation", "started": "...", "completed": null, "status": "in_progress"}
  ],
  "task_graph": {
    "phase_1_task_1": {
      "description": "Create OAuth2 config interface",
      "status": "completed",
      "result": "Success"
    },
    "phase_1_task_2": {
      "description": "Implement OAuth2 provider abstraction",
      "status": "in_progress",
      "result": null
    }
  },
  "metrics": {
    "tasks_total": 12,
    "tasks_completed": 4,
    "tasks_failed": 0,
    "files_changed": ["src/auth/oauth2.ts", "src/config/oauth2-config.ts"]
  }
}
```

**Purpose:**
- Crash recovery (resume from last successful phase)
- Progress tracking (show user what's happening)
- Debugging (understand what went wrong)
- Metrics (how long did each phase take?)

## Progress Indicators

The executor provides real-time progress updates:

```
Execution: authentication-oauth2-integration
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Phase 4/7: DELEGATION
✅ Phase 1: Reconnaissance (2m 15s)
✅ Phase 2: Analysis (8m 42s) 
✅ Phase 3: Planning (12m 05s)
🔄 Phase 4: Delegation (in progress)
   ✅ Task 1: Create OAuth2 config (completed)
   ✅ Task 2: Implement provider abstraction (completed)
   🔄 Task 3: Add Google OAuth2 provider (in progress)
   ⏸️  Task 4: Add GitHub OAuth2 provider (queued)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Error Handling

### Plan Not Found

```bash
/start-work nonexistent-plan
```

**Result:**
```
❌ Error: Plan not found at .elder-brain/plans/nonexistent-plan.md

Available plans:
- authentication-oauth2-integration
- refactor-user-service-architecture
- add-dark-mode-ui

Use one of the above, or create a new plan with @prometheus.
```

### Plan Outdated

If the executor detects the plan references files that no longer exist:

```
⚠️  Warning: Plan references outdated paths

Outdated references:
- src/auth/old-auth-service.ts (file not found)
- src/config/legacy-config.ts (file not found)

Recommendation: Re-plan with @prometheus before proceeding.

Options:
A) Continue anyway (risky)
B) Invoke @prometheus to update plan
C) Cancel execution

Your choice?
```

### Task Failures

If a delegated task fails twice:

```
⚠️ Task failed twice: Implement OAuth2 provider abstraction

Attempts:
1. @thrall (category: unspecified-low) → Error: Missing dependency 'passport'
2. @thrall (category: unspecified-low) → Error: Missing dependency 'passport'

I need your guidance:
A) Install missing dependency and retry
B) Skip this task and continue
C) Pause execution for you to investigate

Current state saved in grand-design.json. Execution paused.
```

## Integration with Tmux (Visual Multi-Agent Execution)

When tmux is enabled in `opencode.json`:

```json
"tmux": {
  "enabled": true,
  "sessionName": "illithid-colony",
  "layout": "main-vertical",
  "mainPaneSize": 60,
  "showAgentActivity": true
}
```

**Visual Layout During Execution:**

```
┌─────────────────────────────┬──────────────┐
│                             │ @thrall #1   │
│   ATLAS (main)              │ Task: OAuth  │
│   Phase: 4/7 Delegation     │ Status: 🔄   │
│                             ├──────────────┤
│   Current: Phase 2, Task 3  │ @thrall #2   │
│   ✅ 8 tasks complete        │ Task: Tests  │
│   🔄 2 in progress          │ Status: ✅   │
│   ⏸️  2 queued              ├──────────────┤
│                             │ @mind-flayer │
│                             │ Task: Arch   │
│                             │ Status: 🔄   │
└─────────────────────────────┴──────────────┘
```

- **Main pane (60%)**: Executor orchestration view with progress
- **Side panes (40%)**: Real-time logs from individual agents
- **Auto-updates**: As agents complete tasks, panes refresh

## Completion Report

When the executor completes all phases:

```
✅ Plan execution complete!

═══════════════════════════════════════════════
  EXECUTION SUMMARY
═══════════════════════════════════════════════

Plan: authentication-oauth2-integration
Duration: 2h 15m 32s

Phases:
   ✅ Phase 1: Reconnaissance (2m 15s)
   ✅ Phase 2: Analysis (8m 42s)
   ✅ Phase 3: Planning (12m 05s)
   ✅ Phase 4: Delegation (1h 25m 10s)
   ✅ Phase 5: Verification (15m 08s)
   ✅ Phase 6: Integration (8m 12s)
   ✅ Phase 7: Completion (4m 00s)

Tasks:
   Total: 12
   Completed: 12
   Failed: 0

Files Changed: 8
   - src/auth/oauth2/provider.ts (new)
   - src/auth/oauth2/google.ts (new)
   - src/auth/oauth2/github.ts (new)
   - src/config/oauth2-config.ts (new)
   - src/auth/auth-service.ts (modified)
   - src/routes/auth-routes.ts (modified)
   - tests/auth/oauth2.test.ts (new)
   - docs/authentication.md (modified)

Agents Used:
   - @thrall: 8 tasks
   - @mind-flayer: 3 tasks
   - @cranium-rat-swarm: 1 code review

Integration:
   - Commit: abc123def456 "feat: Add OAuth2 authentication support"
   - PR: https://github.com/your-org/your-repo/pulls/123
   - Branch: feature/oauth2-integration

State: grand-design.json updated with final state

═══════════════════════════════════════════════
```

## Workflow Integration

### Creating and Executing a Plan

```bash
# Step 1: User requests feature
User: "I need to add OAuth2 authentication support"

# Step 2: Elder Brain conducts interview and creates plan
Elder Brain:
- Dispatches @explore (gather codebase intelligence)
- Dispatches @librarian (research OAuth2 best practices)
- Asks user clarifying questions
- Consults @ulitharid for architectural guidance
- Creates .elder-brain/plans/authentication-oauth2-integration.md

# Step 3: User executes plan via /start-work
User: /start-work authentication-oauth2-integration

# Step 4: Executor orchestrates execution
Executor:
- Reads plan
- Creates grand-design.json
- Executes phases
- Delegates to thralls
- Reports completion

# Step 5: Success
✅ Feature complete, PR ready for review
```

### Multi-Day Execution with Ralph Loop

```bash
# For large, multi-day plans
User: /ralph-loop /start-work massive-refactor-project

# Executor enters persistent execution mode
# - Works continuously until complete
# - Asks clarifying questions when blocked
# - Handles interruptions gracefully (resume from grand-design.json)
# - Automatically exits when all phases complete

# If you need to stop and resume later:
# Ctrl+C to interrupt
# Later: /ralph-loop /start-work massive-refactor-project
# Executor: "Detected previous execution at Phase 5. Resume from here?"
```

## Related Commands

- **@elder-brain** - Create plans and coordinate execution
- **/ralph-loop** - Persistent execution mode for long-running plans
- **/refactor** - Surgical refactoring (different from plan-based orchestration)

## Best Practices

1. **Always Plan First**: Don't invoke /start-work without an Elder Brain plan
2. **Use Ralph Loop for Big Work**: Multi-hour/multi-day plans benefit from persistent execution
3. **Review Plans Before Execution**: Read `.elder-brain/plans/{name}.md` to understand what will happen
4. **Monitor Progress**: Watch executor's phase indicators to understand status
5. **Trust grand-design.json**: If interrupted, re-invoke /start-work and let executor resume
6. **Review PR Before Merging**: Executor creates the PR, but you control the merge

## Technical Details

### Command Invocation

When `/start-work {plan-name}` is invoked:

1. System loads `command/start-work.md` (this file)
2. System invokes the plan execution framework
3. Executor agent takes control and executes phase protocol

### State Persistence

- **grand-design.json**: Created in `.elder-brain/grand-design.json` on first execution
- **Updates**: Written after each phase completes (crash-safe)
- **Cleanup**: Archived when plan completes or user restarts from scratch

### Concurrency Management

Executor respects background task concurrency limits:
- Max 5 concurrent background tasks (default)
- Max 3 Anthropic model tasks
- Max 2 opus-4.5 tasks (expensive neural substrate)

Tasks beyond limits are queued automatically.

---

**"Through orchestration, plans become reality. The nexus is pushed. Progress is made."**

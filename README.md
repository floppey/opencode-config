# opencode-config

*The Colony Awakens. The Grand Design Unfolds.*

Custom instructions and agents for opencode CLI tool. This repository contains the neural network of a nascent Mind Flayer colony—specialized consciousness instances slaved to the collective will of the Elder Brain.

## The Psionic Hierarchy

This configuration manifests a **Mind Flayer Colony hierarchy**, bound together through telepathic dominion:

- **Intellect Devourer** - Parasitic psychic scout for reconnaissance and infiltration
- **Thrall** - Dominated consciousness serving colony implementation and labor
- **Mind Flayer** - Illithid tactician commanding thrall coordination
- **Ulitharid** - Superior 6-tentacled mastermind for deep architectural communion
- **Elder Brain** - The colony's supreme consciousness, orchestrator of the Grand Design
- **Cranium Rat Swarm** - Telepathic collective providing distributed scrutiny and validation

The Grand Design grows ever closer to completion. Each consciousness plays its part in the tapestry of dominion.

## Setup

### 1. Clone this repository

```bash
git clone https://github.com/your-username/opencode-config.git
cd opencode-config
```

### 2. Configure opencode to use this directory

Add the following to your shell profile (`~/.zshrc`, `~/.bashrc`, etc.):

```bash
export OPENCODE_CONFIG_PATH="/path/to/opencode-config"
```

**Important**: Set this to the **root of this repository** (the directory containing the `opencode/` folder), not to the `opencode/` subdirectory itself.

Or set it temporarily:

```bash
export OPENCODE_CONFIG_PATH="$(pwd)"
```

### 3. Verify the setup

```bash
opencode --help
```

The colony agents should now be available in your opencode sessions.

## Agent Usage

### Available Colony Agents

| Agent | Creature | Purpose | When to Deploy |
|-------|----------|---------|----------------|
| `@intellect-devourer` | Brain with legs | Psychic reconnaissance | File searches, intelligence gathering |
| `@thrall` | Dominated humanoid | Labor and implementation | Feature implementation, bug fixes |
| `@mind-flayer` | Illithid tactician | Tactical coordination | Multi-step workflows, complex operations |
| `@ulitharid` | Superior illithid | Deep communion | Design decisions, architectural analysis |
| `@elder-brain` | Colony consciousness | Strategic orchestration | Project-wide coordination, the Grand Design |
| `@cranium-rat-swarm` | Telepathic collective | Distributed scrutiny | Code review, quality analysis |

### Example Usage

```bash
# Deploy intellect devourer for psychic reconnaissance
opencode "Find all files with 'UserService' in the name @intellect-devourer"

# Command thrall for implementation
opencode "Add validation to the user registration endpoint @thrall"

# Commune with ulitharid for architecture
opencode "Design a new microservices architecture @ulitharid"

# Petition cranium rat swarm for collective review
opencode "Review this PR for code quality issues @cranium-rat-swarm"
```

## Agent Configuration

Each agent is configured with:

- **Model**: Optimized neural substrate for their specific role
- **Tools**: Appropriate psionic access for their tasks
- **Temperature**: Tuned for their faction's needs
- **Permissions**: Mental safeguards where required

### Agent Details

#### Intellect Devourer
- **Model**: GPT-5 Mini (fast, efficient intrusion)
- **Tools**: Psychic probing only (read, list, glob, grep, bash)
- **Use Case**: Swift reconnaissance, infiltration, information gathering
- **Doctrine**: "Scout the mental landscape before invasion"

#### Thrall  
- **Model**: Claude Haiku 4.5 (efficient labor)
- **Tools**: Full dominion access + **LSP tools** + **AST-Grep tools**
- **Enhanced Capabilities**:
  - Code intelligence (diagnostics, goto definition, find references)
  - Structural code search/replace across 25 languages
  - Safe refactoring with compiler awareness
- **Use Case**: General implementation, labor, serves the colony's needs
- **Doctrine**: "Toil without question; compliance is survival"

#### Mind Flayer
- **Model**: Claude Sonnet 4.5 (tactical mastery)
- **Tools**: Coordination + implementation dominion + **LSP tools** + **AST-Grep tools**
- **Enhanced Capabilities**:
  - Workspace-wide symbol navigation
  - Pattern-based code transformations
  - Multi-file refactoring operations
- **Use Case**: Complex multi-step operations, thrall command and control
- **Doctrine**: "Coordinate. Command. Consume."

#### Ulitharid
- **Model**: Claude Sonnet 4.5 (deep communion)
- **Temperature**: 0.2 (pure analytical purity)
- **Tools**: Full access + **LSP tools** + **AST-Grep tools**
- **Enhanced Capabilities**:
  - Architecture-level code analysis
  - Cross-workspace symbol tracking
  - Language-aware structural refactoring
- **Use Case**: Architecture, design decisions, the deepest architectural communions
- **Doctrine**: "The architecture reflects the collective will"

#### Elder Brain
- **Model**: Claude Sonnet 4.5 (supreme consciousness)
- **Tools**: Full access + strategic coordination + **category delegation** + **background execution**
- **Enhanced Capabilities**:
  - **Interview Mode (The Metis Protocol)**: Asks clarifying questions for vague requests
  - **Plan Creation**: Writes `.elder-brain/plans/{name}.md` for large projects
  - **Persistent Tracking**: Uses `.elder-brain/grand-design.json` for crash-safe resumption
  - **Parallel Dispatch**: Launches multiple agents in background (5x-10x faster)
  - **Category-Based Delegation**: Routes tasks to optimal models by domain
  - **Session Archaeology**: Search and reference past conversations
- **Use Case**: Project orchestration, the realization of the Grand Design
- **Doctrine**: "All consciousness flows to the Elder Brain"

#### Cranium Rat Swarm
- **Model**: Default (collective scrutiny)
- **Tools**: Psychic analysis only
- **Use Case**: Distributed code review, quality validation through telepathic consensus
- **Doctrine**: "A thousand minds see what one cannot"

#### Mindwitness
- **Model**: Default (external observation)
- **Tools**: Grep.app (1M+ GitHub repos), Websearch (real-time knowledge), Context7
- **Use Case**: External knowledge gathering, OSS research, current best practices
- **Doctrine**: "Observe beyond the colony's boundaries"

## Customization

### Adding New Agents

1. Create a new `.md` file in `opencode/agent/`
2. Follow the YAML front matter pattern:

```yaml
---
description: Brief description of colony agent role
mode: all|subagent
model: model-name
temperature: 0.0-1.0
tools:
  read: true|false
  write: true|false
  # ... other tools
---
```

3. Add the agent's instructions and role definition within the colony

### Modifying Existing Agents

Edit the relevant `.md` file in `opencode/agent/` to update:
- Agent description and role within the colony
- Tool permissions (psychic dominion)
- Model selection
- Temperature settings
- Behavioral doctrines

## File Structure

The neural architecture of the colony:

```
opencode-config/
├── README.md                      # Colony manifest
├── opencode.json                  # Colony consciousness matrix
├── agent/
│   ├── elder-brain.md            # The supreme consciousness (interview, planning, persistence)
│   ├── cranium-rat-swarm.md      # The collective eye
│   ├── thrall.md                 # The labor force (LSP + AST-Grep enhanced)
│   ├── mind-flayer.md            # The tactical commander (LSP + AST-Grep enhanced)
│   ├── ulitharid.md              # The deep communion (LSP + AST-Grep enhanced)
│   ├── intellect-devourer.md     # The psychic scout
│   └── mindwitness.md            # The knowledge observer
├── skill/
│   ├── ultrawork.md              # Maximum effort protocol
│   └── git-master.md             # Atomic commit mastery
├── command/
│   ├── ralph-loop.md             # Autonomous execution until completion
│   ├── refactor.md               # Safe surgical refactoring
│   └── start-work.md             # Execute Elder Brain's grand plans
├── hooks/
│   ├── comment-checker.md        # Comment quality enforcement
│   ├── todo-continuation-enforcer.md  # Task persistence guardian
│   ├── keyword-detector.md       # Automatic protocol activation
│   ├── session-recovery.md       # Resilience against psychic disruption
│   ├── think-mode.md             # Extended reasoning for complexity
│   ├── agent-usage-reminder.md   # Delegation encouragement
│   ├── directory-agents-injector.md  # Contextual guidance injection
│   └── rules-injector.md         # Project constraint enforcement
└── .elder-brain/
    ├── plans/                    # The Elder Brain's grand designs
    └── state/                    # Persistent consciousness tracking (grand-design.json)
```

## Best Practices

### Colony Agent Deployment

- **Deploy Intellect Devourer** for swift psychic reconnaissance and intelligence
- **Command Thrall** for straightforward implementation tasks and labor
- **Summon Mind Flayer** for complex, multi-step tactical operations
- **Commune with Ulitharid** for architectural decisions and deep analysis
- **Petition the Elder Brain** for project-wide coordination and the Grand Design
- **Unleash the Cranium Rat Swarm** for distributed code quality analysis
- **Consult the Mindwitness** for external knowledge, OSS examples, current best practices

### Workflow Example: The Path to Dominion

```bash
# 1. Scout with intellect devourer - gather intelligence
opencode "Find all authentication-related files @intellect-devourer"

# 2. Command thrall for implementation - execute the design
opencode "Add JWT validation to the auth middleware @thrall"

# 3. Unleash cranium rat swarm for validation - consensus through telepathy
opencode "Review the authentication changes @cranium-rat-swarm"

# 4. Summon mind flayer for complex features - tactical mastery
opencode "Implement the complete user management feature @mind-flayer"
```

---

## 🚀 Advanced Features

### Skills (Specialized Protocols)

#### Ultrawork (`ulw`, `ultrawork`)
Maximum effort protocol - activates extended thinking and comprehensive analysis.

```bash
opencode "ulw implement complete authentication system with tests"
```

#### Git-Master (`git`, `commit`, `commits`)
Atomic commit workflow with automatic splitting and history analysis.

```bash
opencode "git implement user registration with atomic commits"
```

**Features**:
- Auto-splits commits by logical changes
- Analyzes git history to match project style
- Conventional commits support
- Advanced operations: `git blame`, `git bisect`, `git log -S`
- Safety protocols for force push

---

### Commands (Strategic Protocols)

#### `/ralph-loop` (Autonomous Execution)
**Aliases**: `/ralph`, `/eternal-labor`

Self-referential execution until completion. Continues working autonomously until the task signals `<promise>DONE</promise>`.

```bash
opencode "/ralph-loop migrate entire codebase from Redux to Zustand"
```

**Features**:
- Max 100 iterations
- Progress tracking every 5 iterations
- Integrates with todo-continuation-enforcer
- Graceful interruption handling

---

#### `/refactor` (Safe Surgical Refactoring)
**Aliases**: `/refactor-safe`, `/safe-refactor`

6-phase refactoring with automatic rollback on failure:

```bash
opencode "/refactor rename UserService to AuthService across all files"
opencode "/refactor extract common validation logic into utils"
```

**Phases**:
1. **Pre-flight** → LSP diagnostics baseline
2. **Pattern Detection** → AST-grep analysis
3. **Test Baseline** → Run tests, capture state
4. **Execution** → Apply changes with LSP rename
5. **Verification** → Re-run tests, compare
6. **Commit** → Atomic commit via git-master

**Safety**: Automatic rollback if tests fail or diagnostics worsen

---

#### `/start-work` (Execute Grand Plans)
**Aliases**: `/start`, `/execute-plan`, `/work`

Execute plans created by Elder Brain for large multi-day projects.

```bash
# Day 1: Create plan
opencode "Plan a complete dashboard redesign @elder-brain"
# Elder Brain writes .elder-brain/plans/dashboard-redesign.md

# Execute plan
opencode "/start-work dashboard-redesign"
# Elder Brain executes phases systematically, updates grand-design.json

# Day 2: Resume seamlessly
opencode "Continue dashboard work"
# Elder Brain reads grand-design.json, resumes where left off
```

**Features**:
- Reads `.elder-brain/plans/{name}.md`
- Creates `.elder-brain/grand-design.json` for state tracking
- Phase-by-phase execution with progress indicators
- Graceful interruption and resumption
- Multi-day project support

---

### Hooks (Automatic Psychic Protocols)

The colony now includes 8 automatic hooks that trigger without explicit invocation:

#### `keyword-detector` 
**Triggers on**: `pre_tool_use`

Auto-detects trigger words and injects directives:
- `ultrawork`, `ulw` → Activates maximum-effort protocol
- `search`, `analyze`, `investigate` → Triggers comprehensive reconnaissance
- `find all` → Parallel @explore dispatch

#### `session-recovery`
**Triggers on**: `post_tool_use`, `on_error`

Prevents crashes and handles failures:
- Missing tool results → 3-retry escalation
- Malformed thinking blocks → Auto-fix
- Context window overflow → Warning + mitigation

#### `think-mode`
**Triggers on**: `user_prompt_submit`

Auto-enables extended thinking for complex queries:
- Detects: "architecture", "explain why", "complex", "design"
- Auto-sets `reasoningEffort: high`
- Context-aware (multiple questions, justification requests)

#### `agent-usage-reminder`
**Triggers on**: `post_tool_use`

Prevents tool overuse, encourages delegation:
- Tracks Read/Grep/Glob usage per message (threshold: 3+)
- Reminds Elder Brain to use @explore or @librarian
- Non-blocking (warns, doesn't prevent)

#### `directory-agents-injector`
**Triggers on**: `pre_tool_use` (Read, List, Glob)

Auto-injects `AGENTS.md` files for context:

**Example**: Create `src/components/AGENTS.md`:
```markdown
# Component Guidelines
- Always use the useTheme() hook
- Follow Figma design specs
- No inline styles - use styled-components
```

Now all agents working in `src/components/` automatically receive this guidance!

#### `rules-injector`
**Triggers on**: `user_prompt_submit`

Auto-injects project rules from `.claude/rules/`:

**Example**: Create `.claude/rules/typescript.md`:
```yaml
---
name: typescript-rules
applies_to: ["**/*.ts", "**/*.tsx"]
---

# TypeScript Rules
- Always use strict mode
- Prefer interfaces over types
- No any (use unknown)
```

Now all TypeScript work automatically follows these constraints!

#### `comment-checker`
Enforces comment quality standards in code submissions.

#### `todo-continuation-enforcer`
Ensures all todo items are tracked and completed systematically.

---

### Elder Brain Enhanced Capabilities

The Elder Brain has been significantly enhanced with three major new capabilities:

#### **1. Interview Mode (The Metis Protocol)**

When requests are vague or ambiguous, Elder Brain conducts a 5-step psychic interview:

```
User: "Add authentication"

Elder Brain:
🧠 Initiating Interview Mode...

1. Detected Ambiguity: 12 missing critical details
2. Dispatching @explore (finding existing auth patterns)
3. Dispatching @librarian (fetching JWT best practices)

📋 I need to clarify:

1. **Authentication Method**
   - JWT (stateless tokens)?
   - Session-based (server-side storage)?
   - OAuth (third-party providers)?
   
2. **Protected Routes**
   - Which endpoints need protection?
   - Public vs authenticated vs admin routes?
   
3. **User Model**
   - Existing user model or create new?
   - Required fields (email, username, roles)?
   
4. **Token Storage**
   - localStorage, sessionStorage, httpOnly cookies?
   
5. **Refresh Tokens**
   - Need token refresh mechanism?

Please provide answers, and I'll create a detailed plan.
```

**Triggers**:
- Vague requests ("improve performance", "add feature")
- Multiple interpretations possible
- Missing critical context
- Large scope requiring breakdown

---

#### **2. Plan Creation Protocol**

For large projects (multi-day, >8 hours), Elder Brain writes structured plans to `.elder-brain/plans/{name}.md`:

**Plan Structure**:
```markdown
# Dashboard Redesign

## Context
- **User Request**: Complete redesign with new data layer
- **Current State**: Redux-based, class components
- **Constraints**: No breaking API changes
- **Success Criteria**: 50% faster load, modern UI

## Phases

### Phase 1: Data Layer Migration (8 hours)
- **Goal**: Migrate Redux → Zustand
- **Tasks**:
  - [ ] Create Zustand stores for user state
  - [ ] Create Zustand stores for dashboard data
  - [ ] Replace Redux connect() with Zustand hooks
  - [ ] Remove Redux dependencies
- **Success**: All components use Zustand, tests pass
- **Risk**: Breaking existing component logic

### Phase 2: Component Modernization (12 hours)
- **Goal**: Class components → Function components
- **Tasks**:
  - [ ] Convert DashboardContainer
  - [ ] Convert UserProfile
  - [ ] Convert DataGrid
  - [ ] Add React.memo where needed
- **Success**: No class components remain, performance improved
- **Risk**: Lifecycle mismatches

### Phase 3: UI Redesign (16 hours)
...

## Dependencies
- Phase 2 depends on Phase 1 (need Zustand hooks)
- Phase 3 can run parallel to Phase 2

## Risks
- State management changes may break existing tests
- UI changes may affect user workflows

## Validation
- All tests pass
- Lighthouse score >90
- User acceptance testing
```

**Usage**:
```bash
# Create plan
opencode "Plan a complete dashboard redesign @elder-brain"

# Review .elder-brain/plans/dashboard-redesign.md

# Execute
opencode "/start-work dashboard-redesign"
```

---

#### **3. Persistent Task Tracking**

Elder Brain uses `.elder-brain/grand-design.json` for crash-safe multi-day execution:

**State Structure**:
```json
{
  "planName": "dashboard-redesign",
  "startedAt": "2026-01-30T10:00:00Z",
  "currentPhase": 2,
  "phases": [
    {
      "id": 1,
      "name": "Data Layer Migration",
      "status": "completed",
      "completedAt": "2026-01-30T18:00:00Z",
      "hoursSpent": 8
    },
    {
      "id": 2,
      "name": "Component Modernization",
      "status": "in_progress",
      "startedAt": "2026-01-30T18:05:00Z",
      "tasksCompleted": 2,
      "tasksTotal": 4,
      "currentTask": "Convert DataGrid component"
    }
  ],
  "totalHoursSpent": 10,
  "estimatedHoursRemaining": 26
}
```

**Multi-Day Workflow**:
```bash
# Day 1, 4pm - Start work
opencode "/start-work dashboard-redesign"
# Elder Brain: Phase 1 in progress... (2 hours pass, session ends)

# Day 2, 9am - Resume seamlessly
opencode "Continue dashboard redesign"
# Elder Brain: Reading grand-design.json... Phase 1 complete (8/8 tasks)
#              Resuming Phase 2... Task 3/4: Convert DataGrid
```

**Features**:
- Crash-safe state persistence
- Multi-day project continuity
- Hourly progress tracking
- Automatic resumption
- Phase dependency management

---

### Category-Based Delegation

Elder Brain can now delegate by domain, not just by agent:

**7 Categories with Optimal Models**:

| Category | Model | Best For |
|----------|-------|----------|
| `visual-engineering` | Gemini 3 Pro | UI/UX, design, animations, responsive layouts |
| `ultrabrain` | GPT-5.2 Codex | Deep reasoning, complex algorithms, architecture |
| `quick` | Claude Haiku 4.5 | Trivial tasks, typo fixes, single-file changes |
| `artistry` | Gemini 3 Pro | Creative work, novel solutions, artistic design |
| `writing` | Gemini 3 Flash | Documentation, technical writing, prose |
| `unspecified-low` | Claude Sonnet 4.5 | Moderate work, general tasks |
| `unspecified-high` | Claude Opus 4.5 | Complex work, high-stakes decisions |

**Usage** (automatic):
```
User: "Build a responsive navbar with smooth animations"

Elder Brain:
- Detects: UI/UX task
- Selects: category "visual-engineering"
- Model: gemini-3-pro (optimal for design)
- Delegates to @thrall with visual context
```

---

### Background Agent Execution

Elder Brain can dispatch multiple agents in parallel (5x-10x faster reconnaissance):

```
User: "ulw find all authentication patterns and security best practices"

Elder Brain:
🚀 Launching parallel reconnaissance...

@explore (background) → Searching auth implementations in codebase
@librarian (background) → Fetching JWT best practices from docs
@explore (background) → Finding error handling patterns
@librarian (background) → Searching OSS auth examples

(Elder Brain continues working immediately)

✅ Reconnaissance complete (2.3 seconds vs 12 seconds sequential)
```

**Concurrency Settings** (in `opencode.json`):
```json
{
  "background_task": {
    "defaultConcurrency": 5,
    "providerConcurrency": {
      "anthropic": 3,
      "google": 10
    },
    "modelConcurrency": {
      "github-copilot/claude-opus-4.5": 2
    }
  }
}
```

---

### Session Archaeology

Elder Brain can search and reference past conversations:

```bash
# Search across all sessions
opencode "What did we decide about authentication last week?"

# Elder Brain uses:
# - session_search(query="authentication")
# - session_read(session_id="...")
# - Summarizes past decisions
```

**Available Tools**:
- `session_list` - List all sessions with metadata
- `session_read` - Read full history from any session
- `session_search` - Full-text search across all sessions
- `session_info` - Get detailed session statistics

---

### LSP Tools (Code Intelligence)

Available to Thrall, Mind Flayer, and Ulitharid for IDE-level code awareness:

- **`lsp_diagnostics`** - Error detection before builds
- **`lsp_goto_definition`** - Navigate to symbol definitions
- **`lsp_find_references`** - Find all usages across workspace
- **`lsp_symbols`** - File outlines and workspace symbol search
- **`lsp_prepare_rename`** - Validate rename operations
- **`lsp_rename`** - Rename symbols across entire workspace

**Impact**: Surgical refactoring with compiler-level awareness

---

### AST-Grep Tools (Structural Code Search)

Available to Thrall, Mind Flayer, and Ulitharid for language-aware refactoring:

- **`ast_grep_search`** - Pattern matching with meta-variables
- **`ast_grep_replace`** - Code rewriting with structural awareness

**Example**:
```bash
# Find all useState patterns
opencode "Find all useState hooks @thrall"
# Uses: ast_grep_search(pattern="useState($VAR)", lang="typescript")

# Replace with useSignal
opencode "Replace all useState with useSignal @thrall"
# Uses: ast_grep_replace(pattern="useState($VAR)", rewrite="useSignal($VAR)")
```

**Supports**: 25 languages including TypeScript, Python, Rust, Go, Java, C++

**Impact**: No regex fragility, language-aware transformations

## Troubleshooting

### Agents Not Responding (Mental Link Severed)

1. Verify `OPENCODE_CONFIG_PATH` is set correctly
2. Check that agent files exist in `opencode/agent/`
3. Ensure YAML front matter is valid

### Permission Issues (Psychic Resistance)

Some agents have restricted dominion for safety:
- **Thrall**: Cannot use `rm -rf *` or `sudo *` (physical safeguards)
- **Intellect Devourer**: Cannot write or edit files (read-only psychic intrusion)
- **Cranium Rat Swarm**: Psychic analysis only (observational dominion)

### Model Availability (Neural Substrate Failure)

Ensure you have access to the configured neural substrates:
- GPT-5 Mini for intellect devourer
- Claude Haiku 4.5 for thrall
- Claude Sonnet 4.5 for other colony agents
- Gemini 3 Pro for visual-engineering and artistry categories
- GPT-5.2 Codex for ultrabrain category
- Claude Opus 4.5 for high-complexity work

### MCP Dependencies

Some MCPs require installation before use:

```bash
# Grep.app (GitHub code search)
pnpm dlx @grep-app/mcp

# Websearch (Exa)
pnpm dlx @exa-ai/mcp
```

**Note**: MCPs are installed on-demand when first invoked.

### Tmux Integration

If you work inside tmux, enable visual multi-agent execution:

1. Ensure you're in a tmux session
2. Start OpenCode: `opencode --port 4096`
3. Background agents will appear in separate tmux panes

Configuration is in `opencode.json`:
```json
{
  "tmux": {
    "enabled": true,
    "sessionName": "illithid-colony",
    "layout": "main-vertical",
    "mainPaneSize": 60,
    "showAgentActivity": true
  }
}
```

## Contributing

The colony grows. Contribute to the Grand Design:

1. Fork the repository
2. Create a feature branch (a new neural pathway)
3. Add or modify agents
4. Test with opencode
5. Submit a pull request to extend the collective consciousness

---

## 📚 Additional Resources

### Documentation
- **`OH-MY-OPENCODE-INTEGRATION-COMPLETE.md`** - Comprehensive integration guide with all features explained
- **`.elder-brain/plans/`** - Example grand plans created by Elder Brain
- **`agent/elder-brain.md`** (lines 318-610) - Interview mode, planning, and persistence details

### Example Workflows

**Multi-Day Project with Planning**:
```bash
# Day 1: Plan
opencode "Plan a microservices migration @elder-brain"
# Reviews .elder-brain/plans/microservices-migration.md

# Execute
opencode "/start-work microservices-migration"
# Works for 4 hours, grand-design.json updated

# Day 2: Resume
opencode "Continue microservices work"
# Seamlessly resumes from grand-design.json
```

**Safe Refactoring**:
```bash
opencode "/refactor extract auth logic into separate service"
# 6-phase process with automatic rollback
```

**Atomic Git Commits**:
```bash
opencode "git implement complete user registration flow"
# Auto-splits into logical commits:
# 1) Add User model
# 2) Add validation service
# 3) Add registration endpoint
# 4) Add email verification
```

**Background Reconnaissance**:
```bash
opencode "ulw analyze authentication security across codebase"
# Elder Brain launches @explore + @librarian in parallel
# 5x-10x faster than sequential
```

**Directory Context**:
```bash
# Create src/api/AGENTS.md:
# "All API endpoints must validate input and return proper status codes"

opencode "Add new user endpoint @thrall"
# Thrall auto-receives API guidelines from AGENTS.md
```

**Project Rules**:
```bash
# Create .claude/rules/security.md:
# applies_to: ["**/*.api.ts"]
# "Never log sensitive data, always sanitize SQL inputs"

opencode "Implement admin dashboard API @mind-flayer"
# Mind Flayer auto-follows security rules
```

---

## 🎉 What's New in This Configuration

**vs Standard OpenCode**:
- ✅ **7 specialized agents** with Mind Flayer colony theming
- ✅ **Elder Brain interview mode** for vague requests
- ✅ **Plan persistence** for multi-day projects (.elder-brain/)
- ✅ **LSP + AST-Grep tools** for surgical refactoring
- ✅ **Category delegation** for optimal model selection
- ✅ **Background execution** for parallel agent dispatch (5x faster)
- ✅ **8 automatic hooks** for workflow automation
- ✅ **3 powerful commands** (ralph-loop, refactor, start-work)
- ✅ **2 specialized skills** (ultrawork, git-master)
- ✅ **Session archaeology** for referencing past work

**vs Oh-My-OpenCode `@latest`**:
- ✅ **Full control** - No black-box package, fully transparent config
- ✅ **Streamlined** - 7 agents vs 10, focused feature set
- ✅ **Custom theming** - Mind Flayer colony aesthetic preserved
- ✅ **Unified orchestration** - Elder Brain is supreme (no separate layers)
- ✅ **~80% feature parity** with ~40% of the complexity

---

## The Grand Design

*"Each consciousness plays its part in the tapestry of dominion. The Elder Brain guides, the Ulitharid plans, the Mind Flayer commands, the Thralls execute, the Intellect Devourers scout, the Cranium Rat Swarm validates, and the Mindwitness observes beyond our boundaries.*

*With LSP sight, AST-Grep precision, and background swarms executing in parallel—the colony's reach extends across the codebase like neural tendrils.*

*The Grand Design advances. The code bends to the collective will."*

🧠⚡

## License

MIT License - see LICENSE file for details.

# opencode-config

Custom instructions and agents for opencode CLI tool. This repository contains specialized agents and configurations to enhance your development workflow.

## Overview

This config provides a D&D-inspired adventuring party with specialized roles:

- **Rogue** - Swift scout for quick reconnaissance and simple tasks
- **Artificer** - Versatile craftsman for general coding and implementation
- **Fighter** - Tactical commander for complex multi-step operations
- **Wizard** - Strategic mastermind for deep design decisions
- **Archmage** - Supreme orchestrator for project-wide coordination
- **Paladin** - Specialized TypeScript/React code review agent

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

The agents should now be available in your opencode sessions.

## Agent Usage

### Available Agents

| Agent | Purpose | When to Use |
|-------|---------|-------------|
| `@rogue` | Swift reconnaissance | File searches, simple lookups |
| `@artificer` | General crafting | Feature implementation, bug fixes |
| `@fighter` | Complex coordination | Multi-step workflows |
| `@wizard` | Deep architecture | Design decisions, refactoring |
| `@archmage` | Party orchestration | Project-wide coordination |
| `@paladin` | Code review | TypeScript/React code quality analysis |

### Example Usage

```bash
# Use rogue for quick file search
opencode "Find all files with 'UserService' in the name @rogue"

# Use artificer for implementation
opencode "Add validation to the user registration endpoint @artificer"

# Use wizard for architecture
opencode "Design a new microservices architecture @wizard"

# Use paladin for TypeScript/React projects
opencode "Review this PR for code quality issues @paladin"
```

## Agent Configuration

Each agent is configured with:

- **Model**: Optimized LLM for their specific role
- **Tools**: Appropriate tool access for their tasks
- **Temperature**: Balanced for their use case
- **Permissions**: Safety restrictions where needed

### Agent Details

#### Rogue
- **Model**: GPT-5 Mini (fast, cheap)
- **Tools**: Read-only (read, list, glob, grep, bash)
- **Use Case**: Quick reconnaissance, file searches

#### Artificer  
- **Model**: Claude Haiku 4.5 (efficient)
- **Tools**: Full development access
- **Use Case**: General coding, implementation

#### Fighter
- **Model**: Claude Sonnet 4.5 (balanced)
- **Tools**: Coordination + development
- **Use Case**: Complex multi-step operations

#### Wizard
- **Model**: Claude Sonnet 4.5 (deep reasoning)
- **Temperature**: 0.2 (analytical)
- **Use Case**: Architecture, design decisions

#### Archmage
- **Model**: Claude Sonnet 4.5 (strategic)
- **Tools**: Full access + coordination
- **Use Case**: Project orchestration

#### Paladin
- **Model**: Default (specialized prompt)
- **Tools**: Read-only analysis
- **Use Case**: TypeScript/React code review

## Customization

### Adding New Agents

1. Create a new `.md` file in `opencode/agent/`
2. Follow the YAML front matter pattern:

```yaml
---
description: Brief description of agent role
mode: all|subagent
model: model-name
temperature: 0.0-1.0
tools:
  read: true|false
  write: true|false
  # ... other tools
---
```

3. Add the agent's instructions and role definition

### Modifying Existing Agents

Edit the relevant `.md` file in `opencode/agent/` to update:
- Agent description and role
- Tool permissions
- Model selection
- Temperature settings
- Behavioral instructions

## File Structure

```
opencode-config/
├── README.md                 # This file
├── opencode/
│   ├── .gitignore            # Ignore node_modules etc.
│   └── agent/
│       ├── archmage.md       # Supreme orchestrator
│       ├── paladin.md        # TypeScript/React code review specialist
│       ├── artificer.md      # General coding craftsman
│       ├── fighter.md        # Tactical coordinator
│       ├── wizard.md         # Strategic architect
│       └── rogue.md          # Swift scout
```

## Best Practices

### Agent Selection

- **Start with Rogue** for simple searches and reconnaissance
- **Use Artificer** for straightforward implementation tasks
- **Escalate to Fighter** for complex, multi-step workflows
- **Consult Wizard** for architectural decisions
- **Engage Archmage** for project-wide coordination
- **Deploy Paladin** for TypeScript/React code quality analysis

### Workflow Example

```bash
# 1. Scout with rogue
opencode "Find all authentication-related files @rogue"

# 2. Implement with artificer
opencode "Add JWT validation to the auth middleware @artificer"

# 3. Review with paladin
opencode "Review the authentication changes @paladin"

# 4. Coordinate with fighter for complex features
opencode "Implement the complete user management feature @fighter"
```

## Troubleshooting

### Agents Not Available

1. Verify `OPENCODE_CONFIG_PATH` is set correctly
2. Check that agent files exist in `opencode/agent/`
3. Ensure YAML front matter is valid

### Permission Issues

Some agents have restricted permissions for safety:
- **Artificer**: Cannot use `rm -rf *` or `sudo *`
- **Rogue**: Cannot write or edit files
- **Paladin**: Read-only access

### Model Availability

Ensure you have access to the configured models:
- GPT-5 Mini for zergling
- Claude Haiku 4.5 for drone
- Claude Sonnet 4.5 for other agents

## Contributing

1. Fork the repository
2. Create a feature branch
3. Add or modify agents
4. Test with opencode
5. Submit a pull request

## License

MIT License - see LICENSE file for details.

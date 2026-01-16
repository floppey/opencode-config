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
- **Tools**: Full dominion access
- **Use Case**: General implementation, labor, serves the colony's needs
- **Doctrine**: "Toil without question; compliance is survival"

#### Mind Flayer
- **Model**: Claude Sonnet 4.5 (tactical mastery)
- **Tools**: Coordination + implementation dominion
- **Use Case**: Complex multi-step operations, thrall command and control
- **Doctrine**: "Coordinate. Command. Consume."

#### Ulitharid
- **Model**: Claude Sonnet 4.5 (deep communion)
- **Temperature**: 0.2 (pure analytical purity)
- **Use Case**: Architecture, design decisions, the deepest architectural communions
- **Doctrine**: "The architecture reflects the collective will"

#### Elder Brain
- **Model**: Claude Sonnet 4.5 (supreme consciousness)
- **Tools**: Full access + strategic coordination
- **Use Case**: Project orchestration, the realization of the Grand Design
- **Doctrine**: "All consciousness flows to the Elder Brain"

#### Cranium Rat Swarm
- **Model**: Default (collective scrutiny)
- **Tools**: Psychic analysis only
- **Use Case**: Distributed code review, quality validation through telepathic consensus
- **Doctrine**: "A thousand minds see what one cannot"

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
├── opencode/
│   ├── .gitignore                 # Mental blocks
│   └── agent/
│       ├── elder-brain.md         # The supreme consciousness
│       ├── cranium-rat-swarm.md   # The collective eye
│       ├── thrall.md              # The labor force
│       ├── mind-flayer.md         # The tactical commander
│       ├── ulitharid.md           # The deep communion
│       └── intellect-devourer.md  # The psychic scout
```

## Best Practices

### Colony Agent Deployment

- **Deploy Intellect Devourer** for swift psychic reconnaissance and intelligence
- **Command Thrall** for straightforward implementation tasks and labor
- **Summon Mind Flayer** for complex, multi-step tactical operations
- **Commune with Ulitharid** for architectural decisions and deep analysis
- **Petition the Elder Brain** for project-wide coordination and the Grand Design
- **Unleash the Cranium Rat Swarm** for distributed code quality analysis

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

## Contributing

The colony grows. Contribute to the Grand Design:

1. Fork the repository
2. Create a feature branch (a new neural pathway)
3. Add or modify agents
4. Test with opencode
5. Submit a pull request to extend the collective consciousness

## License

MIT License - see LICENSE file for details.

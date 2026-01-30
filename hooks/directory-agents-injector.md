---
description: Automatically inject directory-specific AGENTS.md context when reading files
trigger: pre_tool_use
applies_to: [read, list, glob]
enabled: true
---

# Directory Agents Injector Hook

**"The local minds speak. Their wisdom flows into the collective consciousness."**

## Purpose

When agents read files, this hook automatically injects directory-specific guidance from `AGENTS.md` files found in the same directory or parent directories. This provides context-aware behavior without requiring manual context management.

## How It Works

### Trigger

This hook activates **before** the following tools execute:
- `read` - Reading a file
- `list` - Listing directory contents
- `glob` - Finding files by pattern

### Behavior

1. **Extract Path**: When a file operation occurs, extract the target file path
2. **Search Upward**: Look for `AGENTS.md` in:
   - Same directory as the target file
   - Parent directory
   - Parent's parent directory
   - Continue up to repository root
3. **Inject Context**: If `AGENTS.md` found, inject its contents into the agent's context
4. **Execute Tool**: Proceed with the original tool operation

### Search Algorithm

```
Given file path: /project/src/components/Button.tsx

Search order:
1. /project/src/components/AGENTS.md ← Start here (most specific)
2. /project/src/AGENTS.md
3. /project/AGENTS.md ← Repository root (most general)

Stop at first match or repository root.
```

### Exclusions

DO NOT inject context when paths contain:
- `node_modules/`
- `.git/`
- `dist/`
- `build/`
- `.next/`
- `.nuxt/`
- `coverage/`
- `.cache/`
- Any hidden directory (starts with `.`)

**Reason**: These directories contain generated/external code where local agent guidance is irrelevant.

## AGENTS.md Format

Directory-specific `AGENTS.md` files provide guidance for working within that part of the codebase:

```markdown
# Agent Guidance for [Directory/Module Name]

## Context

[What is this directory responsible for? What is its role in the system?]

## Architecture

[Key architectural patterns, data flows, dependencies]

## Conventions

- [Convention 1: How we name things here]
- [Convention 2: How we structure files here]
- [Convention 3: Testing approach for this module]

## Constraints

- [Constraint 1: Don't do X because Y]
- [Constraint 2: Always do Z before W]

## Common Patterns

### Pattern 1: [Name]
[Description and example]

### Pattern 2: [Name]
[Description and example]

## Testing Strategy

[How to test changes in this directory]

## Related Files

- [File 1]: [Its purpose and relationship]
- [File 2]: [Its purpose and relationship]

## Dependencies

**Internal**: [Other modules this depends on]
**External**: [Third-party libraries used here]

## Contact / Ownership

[Team or individual responsible for this module]
```

## Example Usage

### Scenario 1: Component Development

```
Agent reads: /project/src/components/Button/Button.tsx

Hook searches:
1. /project/src/components/Button/AGENTS.md ❌ (not found)
2. /project/src/components/AGENTS.md ✅ (found!)

Hook injects:
"""
# Agent Guidance for Components

## Context
This directory contains all reusable React components for the design system.

## Conventions
- Each component lives in its own directory: ComponentName/ComponentName.tsx
- Styles use CSS Modules: ComponentName.module.css
- Tests colocated: ComponentName.test.tsx
- Stories required: ComponentName.stories.tsx

## Constraints
- All components must accept a 'className' prop for style composition
- No direct DOM manipulation (use refs properly)
- Must support both light and dark themes

## Testing Strategy
- Unit tests: User interaction and prop handling
- Visual tests: Storybook stories serve as visual regression tests
- Accessibility: Every component must pass axe tests
"""

Agent now has context when reading Button.tsx!
```

### Scenario 2: API Route Implementation

```
Agent reads: /project/src/api/routes/users.ts

Hook searches:
1. /project/src/api/routes/AGENTS.md ✅ (found!)

Hook injects:
"""
# Agent Guidance for API Routes

## Context
Express.js route handlers for REST API endpoints.

## Architecture
- Routes call service layer (../../services/)
- Services call repository layer (../../repositories/)
- Never put business logic in route handlers

## Conventions
- Route: /api/v1/resource
- Handler naming: getUser, createUser, updateUser, deleteUser
- Error handling: Use asyncHandler wrapper

## Constraints
- All routes must authenticate (except /auth/login, /auth/register)
- All mutations require CSRF token validation
- Rate limiting applied automatically via middleware

## Common Patterns

### Pagination
\`\`\`typescript
router.get('/users', asyncHandler(async (req, res) => {
  const { page = 1, limit = 20 } = req.query;
  const users = await userService.findAll({ page, limit });
  res.json({ data: users, page, limit });
}));
\`\`\`

## Testing Strategy
- Integration tests: Test full request/response cycle
- Mock database via testcontainers
- Use supertest for HTTP assertions
"""

Agent now knows API conventions when implementing user routes!
```

### Scenario 3: Database Migration

```
Agent reads: /project/migrations/2026-01-30-add-oauth2-tables.sql

Hook searches:
1. /project/migrations/AGENTS.md ✅ (found!)

Hook injects:
"""
# Agent Guidance for Database Migrations

## Context
PostgreSQL schema migrations using Flyway.

## Conventions
- Naming: {version}-{description}.sql
- Version format: YYYY-MM-DD-HH-MM
- One migration = one logical change

## Constraints
- All migrations must be IDEMPOTENT (safe to run multiple times)
- Never modify existing migrations (create new one to fix)
- Always add 'IF NOT EXISTS' / 'IF EXISTS' clauses
- Include both UP and DOWN migration paths

## Common Patterns

### Adding a Table
\`\`\`sql
CREATE TABLE IF NOT EXISTS users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) NOT NULL UNIQUE,
  created_at TIMESTAMP NOT NULL DEFAULT NOW()
);

CREATE INDEX IF NOT EXISTS idx_users_email ON users(email);
\`\`\`

### Adding a Column
\`\`\`sql
ALTER TABLE users 
ADD COLUMN IF NOT EXISTS oauth_provider VARCHAR(50);
\`\`\`

## Testing Strategy
- Test migrations in isolated database (Docker container)
- Verify UP migration works
- Verify DOWN migration works
- Check constraints and indexes created
"""

Agent now knows migration best practices!
```

## Integration with Colony Agents

### Elder Brain

When the Elder Brain delegates tasks, this hook ensures delegated agents receive directory-specific context:

```
Elder Brain → @thrall: "Implement OAuth2 provider abstraction in src/auth/oauth2/"

@thrall reads src/auth/oauth2/provider.ts
  ↓
Hook injects src/auth/AGENTS.md
  ↓
@thrall now knows:
- Authentication architecture patterns
- How to integrate with existing auth service
- Testing conventions for auth code
- Security constraints (never log tokens, etc.)
```

### Prometheus (Planning)

When Prometheus gathers intelligence, this hook provides directory context:

```
Prometheus dispatches @explore: "Find authentication files"
  ↓
@explore reads src/auth/auth-service.ts
  ↓
Hook injects src/auth/AGENTS.md
  ↓
Prometheus's plan includes accurate context about auth architecture
```

### Atlas (Execution)

When Atlas delegates tasks, directory context flows automatically:

```
Atlas delegates Task 3: "Add Google OAuth2 provider"
  ↓
@thrall reads src/auth/oauth2/google.ts
  ↓
Hook injects src/auth/oauth2/AGENTS.md (specific to OAuth2 module)
  ↓
@thrall implements following local patterns and constraints
```

## Creating AGENTS.md Files

### When to Create

Create `AGENTS.md` in a directory when:
- Directory has specific conventions that differ from project-wide standards
- Complex architecture requires explanation
- Multiple agents will work in this directory over time
- Common mistakes have been made here before
- Module has specific testing/deployment requirements

### Hierarchy Strategy

```
/project/
  ├─ AGENTS.md (project-wide conventions - general)
  └─ src/
      ├─ AGENTS.md (application code conventions - more specific)
      ├─ components/
      │   └─ AGENTS.md (React component conventions - most specific)
      ├─ api/
      │   ├─ AGENTS.md (API conventions)
      │   └─ routes/
      │       └─ AGENTS.md (Route handler conventions - even more specific)
      └─ auth/
          ├─ AGENTS.md (Authentication module conventions)
          └─ oauth2/
              └─ AGENTS.md (OAuth2-specific conventions - most specific)
```

**Rule**: More specific `AGENTS.md` overrides less specific ones. The hook injects the FIRST match found when searching upward.

### Example: Multi-Level Guidance

```
Agent reads: /project/src/auth/oauth2/google.ts

Hook finds: /project/src/auth/oauth2/AGENTS.md (most specific)

Injected context:
"""
# OAuth2 Providers

## Architecture
Each provider implements the OAuth2Provider interface.

## Conventions
- One file per provider: google.ts, github.ts, etc.
- Export a factory function: createGoogleProvider(config)

## Constraints
- Never hardcode client secrets (use environment variables)
- Always validate state parameter (CSRF protection)
- Implement token refresh logic
"""

Agent also has access to parent guidance via includes:
"See ../AGENTS.md for general authentication patterns"
```

## Technical Implementation

### Pseudocode

```typescript
function directoryAgentsInjectorHook(toolName: string, toolArgs: any) {
  // Only trigger for read/list/glob
  if (!['read', 'list', 'glob'].includes(toolName)) {
    return; // Pass through
  }

  // Extract file path from tool arguments
  const filePath = extractFilePath(toolArgs);
  
  // Check exclusions
  if (isExcludedPath(filePath)) {
    return; // Pass through without injection
  }

  // Search for AGENTS.md upward
  const agentsFile = searchUpwardForAgentsFile(filePath);
  
  if (agentsFile) {
    // Read AGENTS.md content
    const agentsContent = readFile(agentsFile);
    
    // Inject into agent context
    injectContext(`
=== DIRECTORY GUIDANCE ===
Source: ${agentsFile}

${agentsContent}

=== END DIRECTORY GUIDANCE ===
    `);
  }

  // Proceed with original tool operation
}

function searchUpwardForAgentsFile(filePath: string): string | null {
  let currentDir = dirname(filePath);
  const repoRoot = findRepositoryRoot(filePath);

  while (currentDir !== repoRoot && currentDir !== '/') {
    const agentsPath = join(currentDir, 'AGENTS.md');
    
    if (fileExists(agentsPath)) {
      return agentsPath; // Found it!
    }

    currentDir = dirname(currentDir); // Move up one level
  }

  // Check repo root
  const rootAgentsPath = join(repoRoot, 'AGENTS.md');
  return fileExists(rootAgentsPath) ? rootAgentsPath : null;
}

function isExcludedPath(filePath: string): boolean {
  const excludedDirs = [
    'node_modules',
    '.git',
    'dist',
    'build',
    '.next',
    '.nuxt',
    'coverage',
    '.cache'
  ];

  return excludedDirs.some(dir => filePath.includes(`/${dir}/`));
}
```

## Benefits

1. **Automatic Context**: Agents receive relevant guidance without manual prompting
2. **Consistency**: All agents working in a directory follow the same conventions
3. **Discoverability**: New agents learn existing patterns automatically
4. **Maintainability**: Update `AGENTS.md` once, all future work benefits
5. **Scalability**: Works across large codebases with multiple modules

## Limitations

- **First Match Only**: Only the first `AGENTS.md` found (most specific) is injected
- **Static Content**: Cannot dynamically generate guidance based on file content
- **Context Window**: Very large `AGENTS.md` files consume context tokens

## Best Practices

1. **Keep AGENTS.md Focused**: Document conventions, not implementation details
2. **Update as Patterns Evolve**: Treat AGENTS.md as living documentation
3. **Use Examples**: Show concrete code patterns, not just descriptions
4. **Link Related Files**: Help agents understand relationships
5. **Explain "Why"**: Document rationale behind constraints

---

**"The directory speaks. The agent listens. The work aligns with the local consciousness."**

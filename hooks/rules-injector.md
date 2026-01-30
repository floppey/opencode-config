---
description: Inject project-specific rules from .claude/rules/ based on file patterns
trigger: user_prompt_submit
enabled: true
---

# Rules Injector Hook

**"The laws of the realm are encoded. The collective adheres to the constraints."**

## Purpose

Automatically inject project-specific rules and constraints into agent context based on file patterns. Rules are stored in `.claude/rules/*.md` files with YAML frontmatter defining which files they apply to.

This enables:
- **Type-specific constraints** (e.g., TypeScript rules, SQL rules)
- **Module-specific requirements** (e.g., API rules, component rules)
- **Context-aware guidance** without polluting global agent instructions
- **Project-specific standards** that override general best practices

## How It Works

### Trigger

This hook activates **before** user prompts are processed (at `user_prompt_submit`):

1. User submits prompt
2. Hook analyzes context (files mentioned, current working directory, etc.)
3. Hook scans `.claude/rules/*.md` for matching rules
4. Matching rules are injected into prompt context
5. Agent processes prompt with rules applied

### Rule File Format

Rules files use YAML frontmatter + Markdown body:

```yaml
---
name: typescript-strict-rules
applies_to:
  - "**/*.ts"
  - "**/*.tsx"
  - "!**/*.test.ts"
  - "!**/*.spec.ts"
priority: 10
enabled: true
---

# TypeScript Strict Mode Rules

## Type Safety

- Always use explicit types for function parameters and return values
- Avoid `any` type (use `unknown` if truly dynamic)
- Enable `strict: true` in tsconfig.json
- Use discriminated unions for complex state

## Conventions

- Prefer `interface` over `type` for object shapes
- Use `readonly` for immutable properties
- Prefer `const` assertions for literal types

## Constraints

- Never use `@ts-ignore` (use `@ts-expect-error` with explanation)
- All promises must be explicitly handled (no floating promises)
- No implicit `any` from untyped imports
```

### YAML Frontmatter Properties

| Property | Required | Description | Example |
|----------|----------|-------------|---------|
| `name` | Yes | Unique identifier for this rule set | `typescript-strict-rules` |
| `applies_to` | Yes | Array of glob patterns | `["**/*.ts", "!**/*.test.ts"]` |
| `priority` | No | Injection order (higher = first), default 10 | `20` |
| `enabled` | No | Enable/disable rule, default true | `false` |

### Glob Pattern Syntax

Rules use glob patterns to match files:

| Pattern | Matches |
|---------|---------|
| `**/*.ts` | All TypeScript files recursively |
| `src/**/*.ts` | TypeScript files under `src/` |
| `*.test.ts` | Test files in current directory only |
| `!**/*.test.ts` | EXCLUDE test files |
| `{api,routes}/**/*.ts` | Files in `api/` OR `routes/` directories |

**Negation**: Patterns starting with `!` exclude files from matching.

### Priority System

When multiple rules match, they are injected in priority order:

- **Priority 100+**: Critical constraints (security, compliance)
- **Priority 50-99**: Important project standards
- **Priority 10-49**: General best practices (default: 10)
- **Priority 1-9**: Nice-to-have suggestions

Rules with same priority are injected in alphabetical order by name.

## Example Rules

### Example 1: TypeScript Rules

**File**: `.claude/rules/typescript-rules.md`

```yaml
---
name: typescript-rules
applies_to:
  - "**/*.ts"
  - "**/*.tsx"
  - "!**/*.test.ts"
  - "!**/*.spec.ts"
  - "!**/node_modules/**"
priority: 20
enabled: true
---

# TypeScript Rules

## Type Safety

- Always use explicit return types for exported functions
- Avoid `any` type (use `unknown` if type is truly dynamic)
- Use discriminated unions for complex state modeling

## Async/Await

- Always handle promise rejections
- No floating promises (unhandled async calls)
- Prefer `async/await` over `.then()` chains

## Imports

- Use named imports over default imports
- Group imports: external → internal → relative
- No circular dependencies

## Error Handling

```typescript
// ✅ Good
async function fetchUser(id: string): Promise<User | null> {
  try {
    const response = await api.get(`/users/${id}`);
    return response.data;
  } catch (error) {
    logger.error('Failed to fetch user', { id, error });
    return null;
  }
}

// ❌ Bad (unhandled promise, no return type)
async function fetchUser(id) {
  return api.get(`/users/${id}`);
}
```
```

### Example 2: React Component Rules

**File**: `.claude/rules/react-component-rules.md`

```yaml
---
name: react-component-rules
applies_to:
  - "src/components/**/*.tsx"
  - "src/pages/**/*.tsx"
priority: 15
enabled: true
---

# React Component Rules

## Component Structure

```tsx
// ✅ Correct structure
import type { FC } from 'react';
import styles from './Button.module.css';

interface ButtonProps {
  label: string;
  onClick: () => void;
  variant?: 'primary' | 'secondary';
  disabled?: boolean;
}

export const Button: FC<ButtonProps> = ({ 
  label, 
  onClick, 
  variant = 'primary',
  disabled = false 
}) => {
  return (
    <button 
      className={styles[variant]}
      onClick={onClick}
      disabled={disabled}
    >
      {label}
    </button>
  );
};
```

## Conventions

- **File naming**: PascalCase for components (Button.tsx)
- **Props interface**: ComponentNameProps (ButtonProps)
- **Styles**: CSS Modules (ComponentName.module.css)
- **Tests**: Colocated (ComponentName.test.tsx)

## Constraints

- All components must accept `className` prop for style composition
- No inline styles (use CSS Modules or styled-components)
- No direct DOM manipulation (use refs properly)
- All interactive elements must support keyboard navigation
- Props must be explicitly typed (no implicit any)

## Hooks

- Only call hooks at top level (not in conditionals/loops)
- Exhaustive dependency arrays (no eslint-disable)
- Custom hooks start with "use" prefix
```

### Example 3: SQL Migration Rules

**File**: `.claude/rules/sql-migration-rules.md`

```yaml
---
name: sql-migration-rules
applies_to:
  - "migrations/**/*.sql"
  - "db/migrations/**/*.sql"
priority: 100
enabled: true
---

# SQL Migration Rules

**CRITICAL**: These rules ensure database integrity and zero-downtime deployments.

## Idempotency (REQUIRED)

All migrations MUST be idempotent (safe to run multiple times):

```sql
-- ✅ Good (idempotent)
CREATE TABLE IF NOT EXISTS users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) NOT NULL
);

ALTER TABLE users 
ADD COLUMN IF NOT EXISTS oauth_provider VARCHAR(50);

-- ❌ Bad (not idempotent)
CREATE TABLE users (...);
ALTER TABLE users ADD COLUMN oauth_provider VARCHAR(50);
```

## Naming Convention

Format: `{version}-{description}.sql`
- Version: `YYYY-MM-DD-HH-MM` or sequential number
- Description: Lowercase with hyphens

Examples:
- `2026-01-30-14-30-add-oauth2-tables.sql`
- `001-create-users-table.sql`

## Constraints

- **Never modify existing migrations** (create new one to fix)
- **Always add indexes** for foreign keys
- **Always add NOT NULL constraints** explicitly
- **Never drop columns** (mark deprecated, drop later)
- **Test rollback** (provide DOWN migration if possible)

## Zero-Downtime Patterns

### Adding a Column
```sql
-- Step 1: Add column (nullable initially)
ALTER TABLE users ADD COLUMN oauth_provider VARCHAR(50);

-- Step 2: Backfill data (separate migration)
UPDATE users SET oauth_provider = 'local' WHERE oauth_provider IS NULL;

-- Step 3: Add NOT NULL constraint (separate migration)
ALTER TABLE users ALTER COLUMN oauth_provider SET NOT NULL;
```

### Renaming a Column
```sql
-- Step 1: Add new column
ALTER TABLE users ADD COLUMN email_address VARCHAR(255);

-- Step 2: Copy data
UPDATE users SET email_address = email;

-- Step 3: Application deploys using both columns (transition period)

-- Step 4: Drop old column (separate migration, after deploy complete)
ALTER TABLE users DROP COLUMN email;
```
```

### Example 4: API Security Rules

**File**: `.claude/rules/api-security-rules.md`

```yaml
---
name: api-security-rules
applies_to:
  - "src/api/**/*.ts"
  - "src/routes/**/*.ts"
  - "src/controllers/**/*.ts"
priority: 100
enabled: true
---

# API Security Rules

**CRITICAL SECURITY CONSTRAINTS**

## Authentication

- **All routes** require authentication (except `/auth/login`, `/auth/register`, `/health`)
- Use JWT tokens with short expiration (15 minutes access, 7 days refresh)
- Never store tokens in localStorage (use httpOnly cookies)

## Authorization

- Verify user permissions before any mutation
- Use role-based access control (RBAC)
- Check resource ownership (users can only modify their own data)

## Input Validation

```typescript
// ✅ Good (validated input)
router.post('/users', asyncHandler(async (req, res) => {
  const schema = z.object({
    email: z.string().email(),
    password: z.string().min(8),
    name: z.string().min(1).max(100)
  });

  const validated = schema.parse(req.body);
  const user = await userService.create(validated);
  res.json(user);
}));

// ❌ Bad (unvalidated input)
router.post('/users', async (req, res) => {
  const user = await userService.create(req.body);
  res.json(user);
});
```

## Rate Limiting

- Apply rate limits to all public endpoints
- Stricter limits on auth endpoints (prevent brute force)
- Use Redis for distributed rate limiting

## CSRF Protection

- All mutations require CSRF token validation
- CSRF tokens in httpOnly cookies
- Validate origin header

## SQL Injection Prevention

- **NEVER** concatenate user input into SQL queries
- **ALWAYS** use parameterized queries or ORM

```typescript
// ✅ Good (parameterized)
const user = await db.query(
  'SELECT * FROM users WHERE email = $1',
  [email]
);

// ❌ Bad (SQL injection vulnerable)
const user = await db.query(
  `SELECT * FROM users WHERE email = '${email}'`
);
```

## Sensitive Data

- Never log passwords, tokens, or API keys
- Mask sensitive data in error messages
- Use environment variables for secrets (never hardcode)

## Error Handling

```typescript
// ✅ Good (safe error response)
try {
  const user = await userService.findById(id);
  if (!user) {
    return res.status(404).json({ error: 'User not found' });
  }
  res.json(user);
} catch (error) {
  logger.error('Error fetching user', { error, userId: id });
  res.status(500).json({ error: 'Internal server error' });
}

// ❌ Bad (leaks implementation details)
try {
  const user = await userService.findById(id);
  res.json(user);
} catch (error) {
  res.status(500).json({ error: error.message }); // Leak!
}
```
```

## Context Detection

The hook determines which files are "in context" via:

1. **Explicit File References**: Files mentioned in user prompt
   - "Update src/components/Button.tsx"
   - "Fix the issue in api/routes/users.ts"

2. **Working Directory**: Current directory where agent is operating
   - If agent is in `src/components/`, component rules apply

3. **Recently Modified Files**: Files changed in current session
   - Tracked via tool usage (write, edit operations)

## Injection Format

When rules match, they are injected as:

```
=== PROJECT RULES ===

From: .claude/rules/typescript-rules.md
Applies to: **/*.ts, **/*.tsx

[Rule content here]

───────────────────────────────

From: .claude/rules/react-component-rules.md
Applies to: src/components/**/*.tsx

[Rule content here]

=== END PROJECT RULES ===

[Original user prompt follows]
```

## Integration with Colony Agents

### Elder Brain

When the Elder Brain delegates, rules are automatically applied:

```
User: "Add OAuth2 authentication to the API"

Elder Brain → @thrall: "Implement OAuth2 provider"

Hook detects context: src/api/oauth2.ts (new file)
  ↓
Matches:
  - .claude/rules/typescript-rules.md (applies to *.ts)
  - .claude/rules/api-security-rules.md (applies to src/api/**)
  ↓
Both rules injected into @thrall's context
  ↓
@thrall implements following TypeScript + security constraints
```

### Prometheus (Planning)

Rules influence planning phase:

```
Prometheus creating plan for "Add real-time notifications"

Hook detects plan will involve:
  - src/api/routes/notifications.ts (new)
  - src/websocket/server.ts (new)
  ↓
Matches:
  - .claude/rules/api-security-rules.md
  - .claude/rules/typescript-rules.md
  ↓
Prometheus's plan includes security considerations and type safety requirements
```

### Atlas (Execution)

Rules guide each task delegation:

```
Atlas delegating Task 5: "Create notification API endpoint"

Hook detects: src/api/routes/notifications.ts
  ↓
Matches:
  - .claude/rules/api-security-rules.md (priority 100)
  - .claude/rules/typescript-rules.md (priority 20)
  ↓
Rules injected in priority order (security first, then TypeScript)
  ↓
@thrall implements with authentication, validation, rate limiting, etc.
```

## Creating Rules Files

### When to Create Rules

Create rules when:
- Project has specific standards that differ from general best practices
- Compliance requirements (security, accessibility, etc.)
- Team conventions need enforcement
- Common mistakes need prevention
- Language/framework-specific patterns

### Directory Structure

```
.claude/
└── rules/
    ├── typescript-rules.md
    ├── react-component-rules.md
    ├── api-security-rules.md
    ├── sql-migration-rules.md
    ├── testing-rules.md
    └── accessibility-rules.md
```

### Rule Writing Best Practices

1. **Specific Over Vague**: "Use z.object() for validation" > "Validate inputs"
2. **Examples Over Descriptions**: Show good/bad code examples
3. **Explain Why**: Document rationale behind constraints
4. **Prioritize Correctly**: Security = 100, Standards = 50, Preferences = 10
5. **Keep Focused**: One concern per rule file
6. **Update Regularly**: Rules evolve with project needs

## Combining with Directory Agents

Rules and AGENTS.md files serve different purposes:

| Feature | Rules (`.claude/rules/`) | Directory Agents (`AGENTS.md`) |
|---------|-------------------------|--------------------------------|
| **Purpose** | Constraints & standards | Context & architecture |
| **Trigger** | user_prompt_submit | pre_tool_use (read/list/glob) |
| **Scope** | Global with pattern matching | Directory-specific |
| **Content** | "Don't do X, Always do Y" | "Here's how this module works" |
| **Priority** | Enforcement | Guidance |

**Example**: API Route Implementation

```
Agent implements: src/api/routes/users.ts

Rules Injector:
  ✅ .claude/rules/api-security-rules.md (constraints)
  ✅ .claude/rules/typescript-rules.md (type safety)

Directory Agents Injector:
  ✅ src/api/AGENTS.md (API architecture, patterns, how to test)

Combined context:
  - Security constraints (rules)
  - Type safety requirements (rules)
  - API architecture patterns (directory agents)
  - Existing service/repository structure (directory agents)
```

## Technical Implementation

### Pseudocode

```typescript
function rulesInjectorHook(userPrompt: string, context: Context) {
  // Determine files in context
  const filesInContext = detectFilesInContext(userPrompt, context);
  
  // Find all rule files
  const ruleFiles = findRuleFiles('.claude/rules/');
  
  // Match rules to files in context
  const matchingRules = [];
  
  for (const ruleFile of ruleFiles) {
    const frontmatter = parseYamlFrontmatter(ruleFile);
    
    if (!frontmatter.enabled) continue;
    
    // Check if any file in context matches rule patterns
    for (const file of filesInContext) {
      if (matchesGlobPattern(file, frontmatter.applies_to)) {
        matchingRules.push({
          file: ruleFile,
          priority: frontmatter.priority || 10,
          name: frontmatter.name,
          content: extractMarkdownBody(ruleFile)
        });
        break; // Only add rule once
      }
    }
  }
  
  // Sort by priority (highest first)
  matchingRules.sort((a, b) => b.priority - a.priority);
  
  // Inject rules into prompt context
  if (matchingRules.length > 0) {
    const rulesContext = formatRulesForInjection(matchingRules);
    injectBeforePrompt(rulesContext);
  }
  
  // Continue with prompt processing
}

function matchesGlobPattern(filePath: string, patterns: string[]): boolean {
  for (const pattern of patterns) {
    if (pattern.startsWith('!')) {
      // Exclusion pattern
      if (minimatch(filePath, pattern.slice(1))) {
        return false; // Excluded
      }
    } else {
      // Inclusion pattern
      if (minimatch(filePath, pattern)) {
        return true; // Match!
      }
    }
  }
  return false;
}
```

## Benefits

1. **Automatic Enforcement**: Rules apply without manual reminders
2. **Context-Aware**: Only relevant rules are injected (saves tokens)
3. **Maintainable**: Update rules once, all future work benefits
4. **Discoverable**: New team members learn standards automatically
5. **Flexible**: Enable/disable rules per file pattern

## Limitations

- **Pattern Matching Only**: Cannot detect semantic context (only file paths)
- **Static Rules**: Cannot dynamically adjust based on code content
- **Context Window**: Many rules consume significant tokens

## Best Practices

1. **Start Small**: Add rules incrementally as patterns emerge
2. **High Priority for Security**: Security constraints = priority 100
3. **Provide Examples**: Show concrete good/bad code
4. **Explain Rationale**: Help agents understand the "why"
5. **Test Pattern Matching**: Verify `applies_to` patterns match intended files
6. **Review Regularly**: Update rules as project evolves

---

**"The rules are law. The colony obeys. The code aligns with the Grand Design."**

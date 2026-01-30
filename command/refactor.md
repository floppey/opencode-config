---
name: refactor
aliases: [refactor-safe, safe-refactor]
description: LSP-powered safe refactoring with AST pattern detection and TDD verification
---

# Refactor Command - Architect of Safe Code Transformation

## How to Invoke

Refactor is a **slash command**. Use `/refactor` to execute safe, verified refactoring operations with LSP and AST-grep integration.

### Usage Examples

**Simple rename across codebase:**
```
/refactor rename getUserData to fetchUserProfile
```

**Extract function refactoring:**
```
/refactor extract validation logic from UserForm into validateUserInput function
```

**Pattern-based refactoring:**
```
/refactor replace all console.log with logger.info
```

**Complex multi-file refactoring:**
```
/refactor migrate authentication from session-based to JWT tokens
```

## The Doctrine of Safe Transformation

"Code evolves, but evolution without verification is mutation. The refactor command ensures every transformation preserves behavior, maintains tests, and leaves the codebase healthier than before. This is the colony's commitment to sustainable growth."

When `/refactor` is invoked:

## Phase 1: Pre-Flight Diagnostics (LSP)

**Before touching ANY code**, establish baseline health:

```
1. Run lsp_diagnostics on all affected files
2. Capture current error/warning state
3. Store baseline for comparison

If critical errors exist:
  - Report to user: "Critical errors detected before refactoring"
  - List the errors
  - Ask: "Proceed anyway, or fix errors first?"
```

**This ensures we don't introduce problems—we detect what already exists.**

## Phase 2: Pattern Detection (AST-Grep)

Use `ast_grep_search` to find all instances needing refactoring:

### For Renaming

```typescript
// Find all usages of a function
ast_grep_search({
  pattern: "getUserData($$$)",
  lang: "typescript",
  paths: ["src/"]
})

// Find all usages of a variable
ast_grep_search({
  pattern: "$OBJ.oldPropertyName",
  lang: "typescript",
  paths: ["src/"]
})
```

### For Pattern Replacement

```typescript
// Find console.log usage
ast_grep_search({
  pattern: "console.log($MSG)",
  lang: "typescript"
})

// Find async functions without try-catch
ast_grep_search({
  pattern: "async function $NAME($$$) { $$$ }",
  lang: "typescript"
})
```

### For Architectural Patterns

```typescript
// Find all class components (React)
ast_grep_search({
  pattern: "class $NAME extends Component { $$$ }",
  lang: "typescript"
})

// Find all useState hooks
ast_grep_search({
  pattern: "useState($INIT)",
  lang: "typescript"
})
```

**Present findings to user:**
```
🔍 AST Pattern Analysis Complete

Found [N] instances requiring refactoring:
- [file1.ts]: [line] [snippet]
- [file2.ts]: [line] [snippet]
...

Proceed with refactoring? (yes/no)
```

## Phase 3: Test Baseline (TDD Verification)

**If test suite exists**, run tests BEFORE refactoring:

```bash
# Detect test command from package.json or common patterns
npm test
# OR
pnpm test
# OR
yarn test
# OR
bun test
```

**Store results:**
```
✅ Baseline: [X] tests passing, [Y] tests failing
```

If tests are failing before refactoring:
- Report to user
- Ask if they want to proceed anyway
- Note: "Refactoring will preserve existing test failures"

## Phase 4: Refactoring Execution

### Strategy A: LSP Rename (Safest)

For symbol renaming, use `lsp_rename`:

```typescript
// 1. Prepare rename to verify it's valid
lsp_prepare_rename({
  filePath: "src/utils/user.ts",
  line: 10,
  character: 15
})

// 2. If valid, execute rename
lsp_rename({
  filePath: "src/utils/user.ts",
  line: 10,
  character: 15,
  newName: "fetchUserProfile"
})
```

**LSP rename advantages:**
- Understands scope and references
- Updates imports automatically
- Handles shadowing correctly
- Type-aware

### Strategy B: AST-Grep Replace (Pattern-Based)

For pattern replacement, use `ast_grep_replace`:

```typescript
// Dry run first
ast_grep_replace({
  pattern: "console.log($MSG)",
  rewrite: "logger.info($MSG)",
  lang: "typescript",
  dryRun: true
})

// If dry run looks good, apply
ast_grep_replace({
  pattern: "console.log($MSG)",
  rewrite: "logger.info($MSG)",
  lang: "typescript",
  dryRun: false
})
```

**AST-grep replace advantages:**
- Pattern matching with meta-variables
- Multi-file simultaneous replacement
- Preserves code structure
- Syntax-aware

### Strategy C: Manual Edit (Complex Refactoring)

For complex refactorings requiring logic changes:

1. **Plan the transformation** - Break into steps
2. **Create todo list** - One file/module per todo
3. **Execute incrementally** - One logical change at a time
4. **Run tests after each step** - Verify behavior preserved

## Phase 5: Post-Refactoring Verification

### 5.1: LSP Diagnostics Check

```typescript
// Run diagnostics on all modified files
lsp_diagnostics({
  filePath: "src/utils/user.ts",
  severity: "error"
})
```

**Compare to baseline:**
- ✅ Same or fewer errors: Good
- ❌ New errors introduced: Investigate and fix
- ⚠️ New warnings: Review and assess

### 5.2: Test Suite Verification

```bash
# Run tests again
npm test
```

**Compare to baseline:**
- ✅ All tests still passing: Success
- ❌ New test failures: Refactoring broke something
- 🔄 If failures detected, provide options:
  1. Revert changes
  2. Debug and fix
  3. Update tests (if behavior intentionally changed)

### 5.3: Build Verification

If project has a build step:

```bash
# Run build
npm run build
# OR
pnpm build
# OR
tsc --noEmit  # TypeScript check without output
```

**Ensure build succeeds after refactoring.**

## Phase 6: Commit Recommendation

After successful refactoring, recommend atomic commit:

```
✅ Refactoring complete and verified!

Recommended commit message:
---
refactor: rename getUserData to fetchUserProfile

Updated all references across [N] files to use more
descriptive function name. All tests passing.

Modified files:
- src/utils/user.ts
- src/components/UserProfile.tsx
- src/hooks/useUser.ts
---

Commit now? (yes/no)
```

## Refactoring Patterns Library

### Pattern 1: Function Extraction

**Goal:** Extract repeated code into reusable function

```typescript
// BEFORE (detected pattern):
const result1 = data.filter(x => x.active).map(x => x.id);
const result2 = users.filter(x => x.active).map(x => x.id);

// AFTER (refactored):
const getActiveIds = (items) => items.filter(x => x.active).map(x => x.id);
const result1 = getActiveIds(data);
const result2 = getActiveIds(users);
```

### Pattern 2: Replace Magic Numbers with Constants

```typescript
// Find magic numbers
ast_grep_search({
  pattern: "setTimeout($FUNC, 3000)",
  lang: "typescript"
})

// Refactor to constant
const TIMEOUT_DURATION = 3000;
setTimeout(func, TIMEOUT_DURATION);
```

### Pattern 3: Modernize API Usage

```typescript
// Find old pattern
ast_grep_search({
  pattern: "var $VAR = $VALUE",
  lang: "javascript"
})

// Replace with modern syntax
ast_grep_replace({
  pattern: "var $VAR = $VALUE",
  rewrite: "const $VAR = $VALUE",
  lang: "javascript"
})
```

### Pattern 4: Component Migration (React Class → Hooks)

```typescript
// Find class components
ast_grep_search({
  pattern: "class $NAME extends Component { $$$ }",
  lang: "typescript"
})

// Manual refactoring with steps:
// 1. Convert lifecycle methods to useEffect
// 2. Convert this.state to useState
// 3. Convert this.props to function params
// 4. Test each component after conversion
```

### Pattern 5: Error Handling Addition

```typescript
// Find async functions without try-catch
ast_grep_search({
  pattern: "async function $NAME($$$) { $$$ }",
  lang: "typescript"
})

// Wrap body in try-catch (manual edit with template)
```

## Multi-File Refactoring Workflow

For refactorings spanning many files:

```
1. Create detailed todo list:
   - [ ] Update core module
   - [ ] Update dependent modules
   - [ ] Update tests
   - [ ] Update documentation

2. Execute in dependency order:
   - Start with most depended-upon modules
   - Work outward to dependents
   - This minimizes cascading errors

3. Run tests after each module:
   - Catch breakage early
   - Isolate problematic changes

4. Commit in logical groups:
   - One commit per module or layer
   - Or one commit for entire refactor if atomic
```

## Safety Guardrails

### Automatic Rollback

If verification fails:

```
❌ Refactoring verification failed!

[N] new errors introduced:
- [error details]

Options:
1. Rollback changes (git restore)
2. Attempt to fix errors
3. Continue anyway (not recommended)

Choose: 
```

### Backup Before Large Refactors

For complex refactorings:

```bash
# Create backup branch
git checkout -b backup-before-refactor
git checkout -

# Now safe to refactor on main branch
# If things go wrong: git reset --hard backup-before-refactor
```

## Integration with Other Features

### Refactor + Git-Master

```
/refactor with @git-master: migrate API endpoints
```

Result: Safe refactoring with atomic commits for each logical change

### Refactor + Ralph-Loop

```
/ralph-loop /refactor entire authentication system
```

Result: Persistent refactoring that continues until complete

### Refactor + Think-Mode (Auto-Triggered)

Complex refactorings automatically enable extended thinking for architectural decisions

## Performance Considerations

### For Large Codebases

1. **Limit scope with paths:**
```typescript
ast_grep_search({
  pattern: "console.log($MSG)",
  lang: "typescript",
  paths: ["src/components/"]  // Limit to specific directory
})
```

2. **Batch file processing:**
- Process files in groups
- Run diagnostics per batch
- Avoid overwhelming LSP server

3. **Incremental commits:**
- Commit after each major step
- Enables easier rollback if needed

## Philosophy

"Refactoring is the colony's practice of controlled evolution. The codebase is a living organism—it must adapt to new requirements, new knowledge, new thralls. But evolution without verification is chaos. The refactor command embodies the colony's discipline: measure twice, cut once. Verify always."

**The Three Laws of Safe Refactoring:**

1. **Preserve Behavior** - Tests must pass before and after
2. **Improve Structure** - Code should be cleaner after refactoring
3. **Maintain Safety** - No new errors introduced

## Examples

### Example 1: Simple Rename

**Input:**
```
/refactor rename calculateTotal to computeOrderTotal
```

**Execution:**
```
🔍 Phase 1: Pre-flight diagnostics
✅ No critical errors detected

🔍 Phase 2: Finding all usages
✅ Found 8 usages across 4 files

🔍 Phase 3: Test baseline
✅ 24 tests passing

🔄 Phase 4: Executing LSP rename
✅ Renamed in all 8 locations

🔍 Phase 5: Verification
✅ LSP diagnostics: No new errors
✅ Tests: 24 tests still passing
✅ Build: Success

✅ Refactoring complete!

Recommended commit:
refactor: rename calculateTotal to computeOrderTotal

Improved function name clarity for order calculations.
All tests passing.

Commit now?
```

### Example 2: Pattern Replacement

**Input:**
```
/refactor replace all var declarations with const
```

**Execution:**
```
🔍 Phase 1: Pre-flight diagnostics
✅ Baseline established

🔍 Phase 2: AST pattern search
✅ Found 47 var declarations

🔄 Phase 3: Dry run
[Shows preview of changes]

Proceed? yes

🔄 Phase 4: Applying replacements
✅ Replaced 47 instances

🔍 Phase 5: Verification
✅ LSP diagnostics: No new errors
✅ Tests: All passing
✅ Build: Success

✅ Refactoring complete!
```

---

**"The codebase evolves. The colony adapts. The refactor command ensures evolution serves the Grand Design."**

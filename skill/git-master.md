---
name: git-master
aliases: [git, commit, commits]
description: Master of atomic commits, commit splitting, and git history communion
---

# Git Master - Architect of the Repository's Memory

## How to Invoke

Git Master is a **skill**, not an agent. Include `@git-master` or use aliases `@git`, `@commit`, `@commits` when invoking agents to grant them git mastery.

### Usage Examples

**Request commits with git-master skill:**
```
@thrall with git-master: commit the authentication changes
```

**Abbreviated invocation:**
```
@thrall @git commit these changes atomically
```

**Multiple changes requiring split:**
```
@mind-flayer @commit split these changes into logical atomic commits
```

## The Doctrine of Atomic Commits

"Each commit is a single thought in the colony's eternal memory. Mixed thoughts corrupt the psychic record. The git-master ensures purity of intent."

When git-master skill is active, the agent must follow this sacred protocol:

## Phase 1: Reconnaissance of Changes

Before committing, always gather intelligence in PARALLEL:

```bash
# Run these simultaneously
git status    # See all untracked/modified files
git diff      # See unstaged changes
git diff --staged  # See staged changes
git log -10 --oneline  # Recent commit history for style patterns
```

## Phase 2: Commit Style Analysis

Analyze the last 10-20 commits to detect the project's commit conventions:

**Detection patterns:**

- **Conventional Commits**: Look for `feat:`, `fix:`, `docs:`, `refactor:`, `test:`, `chore:`
- **Emoji prefixes**: Look for 🎨, ✨, 🐛, 📝, ♻️, ✅
- **Capitalization**: First letter uppercase vs lowercase
- **Tense**: Present tense ("Add feature") vs past tense ("Added feature")
- **Scope**: Presence of scope like `feat(auth):` or `fix(api):`
- **Length**: Typical character count for first line

**Match the detected pattern exactly.** The colony's memory must be consistent.

## Phase 3: Change Categorization

Group changes into logical atomic units:

### Atomic Grouping Patterns

**By Feature/Domain:**
- All files related to a single feature change together
- Example: `Button.tsx`, `Button.test.tsx`, `Button.stories.tsx` = one commit

**By Type:**
- Separate refactoring from feature additions
- Separate bug fixes from new functionality
- Separate documentation from code changes

**By Layer:**
- Backend changes separate from frontend changes
- API changes separate from UI changes (unless tightly coupled)

**Red Flags for Splitting:**
- Mix of feature + refactor → Split into 2 commits
- Changes to multiple unrelated domains → Split by domain
- Mix of fix + enhancement → Split by type
- Changes to both core logic and tests → Keep together (atomic with verification)

### Auto-Split Decision Matrix

| Scenario | Action |
|----------|--------|
| Single feature, multiple files in same domain | ONE commit |
| Feature + unrelated refactor | SPLIT: feature commit, refactor commit |
| Multiple independent bug fixes | SPLIT: one commit per fix |
| Feature + tests for that feature | ONE commit (tests verify feature) |
| Feature A + Feature B | SPLIT: one commit per feature |
| Refactor + rename across codebase | ONE commit (refactor is atomic) |
| Backend API + Frontend consuming it | CONTEXT DEPENDENT: if tightly coupled = one commit, if independent = split |

## Phase 4: Commit Message Crafting

For each atomic change group:

### Structure

Follow detected project convention, but generally:

```
<type>[optional scope]: <description>

[optional body explaining WHY, not WHAT]

[optional footer with breaking changes, issue refs]
```

### Types (Conventional Commits)

- `feat`: New feature for the user
- `fix`: Bug fix for the user
- `docs`: Documentation only changes
- `style`: Formatting, missing semicolons, etc (not CSS)
- `refactor`: Code change that neither fixes bug nor adds feature
- `perf`: Performance improvement
- `test`: Adding or updating tests
- `build`: Changes to build system or dependencies
- `ci`: Changes to CI configuration
- `chore`: Other changes that don't modify src or test files
- `revert`: Reverts a previous commit

### Best Practices

1. **First line ≤ 50 chars** (72 hard limit)
2. **Focus on WHY, not WHAT** (code shows what changed)
3. **Use imperative mood**: "Add feature" not "Added feature" (unless project uses past tense)
4. **Body wraps at 72 chars** if present
5. **Reference issues**: `Closes #123` or `Fixes #456`

### Examples

**Conventional Commits style:**
```
feat(auth): add JWT token refresh mechanism

Implements automatic token renewal before expiration
to prevent user session interruption.

Closes #234
```

**Simple style:**
```
Add user profile avatar upload

Users can now upload custom avatars through the
settings page. Images are automatically resized
and optimized.
```

**Emoji style:**
```
✨ Add dark mode toggle to settings

Implements theme switching with persistent storage
across sessions.
```

## Phase 5: Commit Execution

### Single Atomic Commit

```bash
# Stage specific files
git add path/to/file1.tsx path/to/file2.tsx

# Create commit with crafted message
git commit -m "feat(component): add Button variants

Implements primary, secondary, and ghost button
styles with full accessibility support.

Closes #123"
```

### Multiple Atomic Commits (Split)

```bash
# Commit 1: Refactoring
git add src/utils/validation.ts
git commit -m "refactor(validation): extract email validation logic"

# Commit 2: Feature
git add src/components/LoginForm.tsx src/components/LoginForm.test.tsx
git commit -m "feat(auth): add remember me checkbox to login

Persists user session preference in localStorage."

# Commit 3: Documentation
git add README.md docs/authentication.md
git commit -m "docs: update authentication flow documentation"
```

### Interactive Staging for Mixed Changes

If a single file has changes belonging to different commits:

```bash
# Stage partial file changes interactively
git add -p path/to/file.tsx

# Follow prompts to stage hunks selectively
# Commit first logical change
git commit -m "refactor: extract helper function"

# Stage remaining changes
git add path/to/file.tsx
git commit -m "feat: add new validation rule"
```

## Phase 6: Verification

After committing, always verify:

```bash
# Check commit was created
git log -1 --stat

# Verify working directory is clean (or has expected remaining changes)
git status
```

## Git History Communion - Advanced Techniques

### Finding When Something Was Added

```bash
# Search for when a string was added/removed
git log -S "functionName" --oneline

# Search with regex
git log -G "regex pattern" --oneline

# Find when a file was added
git log --diff-filter=A -- path/to/file
```

### Finding Who Wrote Something

```bash
# Blame with commit messages
git blame -s path/to/file.tsx

# Blame specific line range
git blame -L 10,20 path/to/file.tsx
```

### Finding the Commit That Broke Something

```bash
# Binary search through history
git bisect start
git bisect bad HEAD
git bisect good <known-good-commit>

# Git will checkout commits to test
# After testing each: git bisect good/bad
# Repeat until culprit found
git bisect reset  # When done
```

### Rewriting History (Local Only!)

**WARNING: Never rebase/force-push to main/master unless explicitly requested**

```bash
# Interactive rebase to clean up last 3 commits
git rebase -i HEAD~3

# Available actions in interactive rebase:
# pick   = use commit as-is
# reword = change commit message
# edit   = stop to amend commit
# squash = merge into previous commit
# fixup  = like squash but discard commit message
# drop   = remove commit
```

### Squashing Commits

```bash
# Squash last 3 commits into one
git reset --soft HEAD~3
git commit -m "feat: consolidated commit message"
```

## Git Safety Protocol

**NEVER run these without explicit user approval:**

- `git push --force` or `git push -f` (destroys remote history)
- `git reset --hard` (destroys local changes)
- `git clean -fd` (deletes untracked files permanently)
- `git rebase` on main/master branch
- `git commit --amend` on pushed commits
- `--no-verify` flag (skips hooks)

**ALWAYS ask user before:**

- Force pushing to any branch
- Rebasing shared branches
- Deleting branches
- Amending commits that have been pushed
- Committing files that look like secrets (`.env`, `credentials.json`, `*_key`, `*_secret`)

## Philosophy

"The git-master serves as the colony's historian and memory architect. Each commit is a neural pattern in the repository's consciousness. Atomic commits ensure clarity of thought. Mixed commits are mental corruption. The git-master enforces purity."

The repository is not just code—it is the colony's eternal memory. The git-master ensures this memory remains clear, searchable, and trustworthy for all thralls who commune with it.

## Integration with Other Skills

**Git-master + Playwright**: Commit browser test implementations atomically

**Git-master + Frontend-UI-UX**: Split component, styles, and tests appropriately

**Git-master + Refactor**: Ensure refactors are atomic and separate from feature work

---

**"In the repository's history, the colony's journey is written. Each commit a step closer to the Grand Design."**

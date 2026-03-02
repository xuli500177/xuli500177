# CLAUDE.md

This file provides guidance for AI assistants (Claude and others) working in this repository.

## Repository Overview

**Repository:** xuli500177/xuli500177
**Status:** Freshly initialized — no application code exists yet. The repository contains only a `.gitkeep` placeholder.

This is a blank-slate project. When new code is added, update this file to reflect the actual stack, structure, and conventions.

---

## Git Workflow

### Branch Naming

Feature branches created by Claude Code must follow this pattern:

```
claude/<descriptive-slug>-<SESSION_ID>
```

Example: `claude/add-claude-documentation-MVSKZ`

The session ID suffix is required — pushes to branches that deviate from this pattern will be rejected with HTTP 403.

### Standard Operations

```bash
# Create and switch to a feature branch
git checkout -b claude/<slug>-<SESSION_ID>

# Stage specific files (avoid git add -A or git add . to prevent accidental secrets)
git add <file1> <file2>

# Commit with a descriptive message
git commit -m "Short imperative summary

Longer explanation if needed."

# Push and set upstream tracking
git push -u origin claude/<slug>-<SESSION_ID>
```

### Push Retry Policy

If a push fails due to a **network error**, retry with exponential backoff:

| Attempt | Wait before retry |
|---------|-------------------|
| 1       | 2 s               |
| 2       | 4 s               |
| 3       | 8 s               |
| 4       | 16 s              |

Do **not** retry on HTTP 403 (permission/branch naming issue) — investigate the cause instead.

### Never Do

- Force-push to `master` or any shared branch
- Use `--no-verify` to bypass commit hooks without explicit user permission
- Push to a branch other than the one designated for the current session
- Commit `.env` files, credentials, or other secrets

---

## Development Principles

### Keep Changes Minimal

- Only modify what was explicitly requested
- Do not refactor surrounding code during bug fixes
- Do not add docstrings, comments, or type annotations to untouched code
- Do not introduce feature flags or backwards-compatibility shims unless required

### Avoid Over-Engineering

- Prefer the simplest solution that satisfies the requirements
- Three similar lines of code is better than a premature abstraction
- Do not create helpers or utilities for one-off operations
- Do not design for hypothetical future requirements

### Security

- Never introduce command injection, XSS, SQL injection, or other OWASP Top 10 vulnerabilities
- Validate input only at system boundaries (user input, external APIs)
- Trust internal framework guarantees; avoid defensive coding for impossible states
- Do not hardcode credentials or secrets anywhere in the codebase

---

## Working with an Empty Repository

Because this repository has no application code yet, the following applies until a stack is chosen and documented:

1. **Before writing any code**, confirm the intended language, framework, and project structure with the user.
2. **After scaffolding**, update this CLAUDE.md with:
   - The actual directory layout
   - How to install dependencies
   - How to run the application
   - How to run tests and linters
   - Any environment variable requirements
3. **Use the project's own conventions** once established — do not impose opinionated defaults without agreement.

---

## Updating This File

Keep CLAUDE.md current. Whenever the project structure, tooling, or conventions change, update the relevant sections here as part of the same commit. Outdated documentation is worse than no documentation.

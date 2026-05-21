# Git Conventions
**Status:** Active
**Last updated:** 2026-05-21

---

## Commit Messages — Conventional Commits

Format:
```
<type>(<scope>): <description>

[optional body]
[optional footer]
```

### Types
| Type | Use for |
|---|---|
| `feat` | New feature or capability |
| `fix` | Bug fix |
| `chore` | Maintenance, tooling, config |
| `docs` | Documentation only |
| `test` | Adding or fixing tests |
| `refactor` | Code change that is neither fix nor feature |
| `perf` | Performance improvement |
| `ci` | CI/CD changes |

### Scope
The affected module or component. Examples:
- `feat(dynamics): implement gain computer`
- `fix(filters): correct Butterworth coefficient calculation`
- `chore(deps): bump SDK to v0.2.0`

### Rules
- Description: imperative mood, lowercase, no period
- Body explains *why*, not *what*
- One commit per stage/phase — not per file

---

## Branching

### Branch naming
```
stage{NN}_phase{N.N}_{short_description}
```

### Rules
- `main` is always buildable and passing
- Branch per phase, merge on phase completion
- No long-lived feature branches
- Delete branch after merge

---

## Tagging — SDKs

```
v{MAJOR}.{MINOR}.{PATCH}
```

### Rules
- Tag on `main` only
- Annotated tags: `git tag -a v0.1.0 -m "Release v0.1.0"`
- Consumers always pin to a tag — never to a branch or SHA
- See `versioning_policy.md` for what constitutes a breaking change

---

## .gitignore

Generated via `SCRIPTS/generate_gitignores.py` at repo root.
Never hand-edit unless adding project-specific entries.

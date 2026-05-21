# Versioning Policy
**Status:** Active
**Last updated:** 2026-05-21
**Applies to:** SDK-TemporalDSPKit, SDK-TemporalDSPUI

---

## Semantic Versioning

SDKs follow [Semantic Versioning 2.0.0](https://semver.org):

```
v{MAJOR}.{MINOR}.{PATCH}
```

| Segment | Increment when |
|---|---|
| MAJOR | Public API breaking change |
| MINOR | New public API added, backwards compatible |
| PATCH | Bug fix, no API change |

---

## What Counts as a Breaking Change

- Removing or renaming a public type, method, or property
- Changing a public method signature
- Changing a parameter range that affects existing DSP output
- Changing a default value that affects existing DSP output
- Removing a module

**Not breaking:**
- Adding a new public type, method, or module
- Internal refactoring with identical public behaviour
- Performance improvements with identical output

---

## Pre-Release (below v1.0.0)

- MINOR bumps may contain breaking changes
- Every breaking change must be documented in `CHANGELOG.md`
- Consumers must read the changelog before bumping their pin
- v1.0.0 signals API stability — breaking changes always increment MAJOR after that

---

## Consumer Pin Rules

- Always pin to an exact tag in `Package.swift`
- Never pin to a branch or commit SHA
- Update pins deliberately — read `CHANGELOG.md` before bumping

---

## Tagging Procedure

```bash
git checkout main
swift test

git tag -a v0.1.0 -m "Release v0.1.0 — {brief description}"
git push origin v0.1.0
```

After tagging:
1. Update `CHANGELOG.md` — move Unreleased items under the new version
2. Append to `DOCS/API/surface_update.log` if public API changed
3. Notify consumer projects to evaluate the pin bump

# TemporalDSP — Agent Bootstrap Reference
**Status:** Living document
**Last updated:** 2026-05-21

---

## Purpose

Shared baseline for all agentic sessions across the TemporalDSP ecosystem.
Referenced by every project's `init_thread.md`.

Read this once at session start. It defines the rules, the structure,
and where to find what you need. Do not proceed without reading it.

---

## Governance Rules — Non-Negotiable

These rules apply to every project, every session, without exception:

1. Top-level `TemporalDSP/` is never a git repo
2. One project = one repo = one GitHub remote
3. SDKs are versioned Swift Packages — consumers pin by tag, never by branch
4. No git submodules — Swift Package Manager handles all SDK dependencies
5. SDK features must exist and be tested before being implemented in any product
6. Rust is reserved for the legacy License Manager only — everything else is Swift
7. No commercial release until M5 Studio is acquired and Apple Silicon validated
8. `STAGING/` is local only — never pushed, never referenced in any remote
9. `Package.resolved` — never commit in SDK libraries, always commit in AU/App projects

---

## Stack Reference

| Domain | Technology |
|---|---|
| DSP / AUv3 / Apps | Swift 6, Swift Package Manager |
| Licensing (legacy) | Rust · Tauri · React/TypeScript |
| Licensing (next) | Swift — deferred until first AUv3 beta complete |
| Scripts | Python 3 |
| Cloud | Cloudflare Workers · Firebase Spark · Stripe |
| IDE | Xcode · VS Code |

---

## Repo Map

| GitHub Remote | Local Path | Type |
|---|---|---|
| `temporaldsp-admin/SDK-TemporalDSPKit` | `SDK/TemporalDSPKit` | Swift Package (library) |
| `temporaldsp-admin/SDK-TemporalDSPUI` | `SDK/TemporalDSPUI` | Swift Package (library) |
| `temporaldsp-admin/AU-{plugin}` | `AU/{plugin}` | AUv3 Xcode project |
| `temporaldsp-admin/APP-{app}` | `APP/{app}` | macOS application |
| `temporaldsp-admin/DOCS` | `DOCS/` | Documentation |

---

## Conditional Document Fetches

Fetch only when your task requires it — do not load everything by default:

| Task type | Fetch |
|---|---|
| DSP implementation | `PUBLIC_DOCS/STANDARDS.md` |
| Public SDK API change | `PUBLIC_DOCS/contracts/TemporalDSPKit_public_api.md` |
| UI SDK API change | `PUBLIC_DOCS/contracts/TemporalDSPUI_public_api.md` |
| Security-sensitive change | `PUBLIC_DOCS/SECURITY.md` |
| Commit / branch / tag work | `PUBLIC_DOCS/conventions/git_conventions.md` |
| New Swift file / naming | `PUBLIC_DOCS/conventions/swift_conventions.md` |
| SDK version bump | `PUBLIC_DOCS/conventions/versioning_policy.md` |

---

## Session Protocol

### Before writing any code
1. Confirm the current stage and phase for this project
2. Read the project's `init_thread.md` in project knowledge
3. Fetch only the conditional documents relevant to your task

### Committing
- One commit per phase
- Conventional Commits format — see `conventions/git_conventions.md`
- All tests must pass before committing to main

### Ending a session
- Mid-phase: write a handover note in project local knowledge
- Phase complete: commit, tag if applicable, update `CHANGELOG.md`
- Public API changed: append to `DOCS/API/surface_update.log` locally

---

## Roadmap Position (May 2026)

```
Phase 0  ACTIVE   SDK hardening + first AUv3 plugin beta
Phase 1  PENDING  License Manager (Swift) — deferred until AUv3 beta
Phase 2  2027     M5 acquisition → first commercial releases
Phase 3  2027+    Expanding the AUv3 ecosystem
```

---

## What This Document Does Not Contain

- Product names or release dates
- Internal architecture or implementation detail
- Threat models, attack trees, or cloud specifics
- Anything that would inform a competitor or attacker

All of the above lives in project-specific local knowledge only.

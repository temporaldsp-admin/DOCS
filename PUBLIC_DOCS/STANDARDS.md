# TemporalDSP — Engineering Standards
**Status:** Living document
**Owner:** Solo dev
**Last updated:** 2026-05-21

---

## Purpose

Front-door reference for engineering quality across the TemporalDSP ecosystem.
Agents bootstrap from this document. Humans onboarding start here.

This document states *what* the standards are and *where* the enforcement
lives. It does not contain implementation detail — that lives with each
component.

---

## Quality Model

TemporalDSP adopts **ISO/IEC 25010** as its reference quality framework.
All components are evaluated against these dimensions:

| Dimension | What it means here |
|---|---|
| Functional suitability | Does it do what the spec says, verified by tests? |
| Performance efficiency | Meets real-time audio constraints, benchmarked |
| Reliability | No crashes under normal host conditions |
| Security | Follows SECURITY.md standing principles |
| Maintainability | Readable by a fresh agent with no prior context |
| Portability | Builds clean on Intel today, Apple Silicon target |
| Compatibility | AUv3 host compatibility, SPM version pinning |

---

## Code Standards

### Swift
- **Style:** Apple Swift API Design Guidelines
  https://swift.org/documentation/api-design-guidelines/
- **Lint:** SwiftLint — config at `.swiftlint.yml` in each repo
- **Format:** SwiftFormat — config at `.swiftformat` in each repo
- **Language version:** Swift 6, strict concurrency enabled
- **Package manager:** Swift Package Manager only — no CocoaPods, no Carthage

### Rust (License Manager only)
- **Style:** Rust API Guidelines
- **Format:** `rustfmt` — config at `rustfmt.toml`
- **Lint:** `clippy` — warnings treated as errors in CI

### Python (Scripts only)
- **Style:** PEP 8
- **Format:** `black`
- **Scope:** Scripts only — never in shipped products

---

## Repository Standards

### Every repo must contain
- `README.md` — purpose, status, current stage/phase, build instructions
- `CHANGELOG.md` — Keep a Changelog format
- `.gitignore` — stack-appropriate, generated via `SCRIPTS/generate_gitignores.py`
- `.swiftlint.yml` — for Swift repos
- `.swiftformat` — for Swift repos
- `.editorconfig` — all repos

### Naming conventions
- SDK libraries: `SDK-{Name}` — e.g. `SDK-TemporalDSPKit`
- AUv3 plugins: `AU-{Name}`
- macOS apps: `APP-{Name}`
- Docs: `DOCS`

### Branch model
- `main` — always buildable, always passing tests
- Feature work on `stage{NN}_phase{N.N}_{description}` branches
- Merge to main at phase completion, after tests pass
- No long-lived feature branches

---

## Testing Standards

### DSP components (TemporalDSPKit)
Every DSP component requires two test files:
- `{Component}CorrectnessTests.swift` — mathematical correctness
- `{Component}CharacterTests.swift` — sonic/perceptual character

### Coverage targets
| Component type | Minimum coverage |
|---|---|
| DSP algorithms | 90% |
| UI components | 60% |
| App logic | 70% |
| Scripts | No formal target |

### Test results
- Archived in `Tests/TestResults/` with git hash in filename
- Run via `Scripts/TestScripts/run_tests.sh`
- All tests must pass before merging to main

---

## Session Standards (Agentic Engineering)

### Stage/phase naming
```
stage01_phase1.1_projectsetup
stage02_phase2.1_implementation
```

### Per-session rules
1. Confirm current stage and phase before writing any code
2. One commit per phase — not per file, not per function
3. Commit message format: Conventional Commits (see `conventions/git_conventions.md`)
4. End every session with a handover note if state is mid-phase
5. Never start a session without reading `init_thread.md` for the project

### Agentic contract discipline
- Before modifying any public SDK API surface: read the relevant contract in `contracts/`
- Before changing parameter ranges or defaults: the spec in that project is locked
- Any public API change requires a `surface_update.log` entry (local API/ folder)

---

## Documentation Standards

### Public API documentation
- Swift Packages: DocC inline documentation on all public symbols
- Format: `/// Summary line.` + `/// - Parameters:` + `/// - Returns:`
- All public types, methods, and properties must be documented

### Specification files
- Live alongside the component they describe
- Format: Markdown
- Header must include: status (LOCKED / DRAFT), last updated date
- LOCKED specs require updates in all consumer repos before merging

### Handover documents
- Written at the end of any session that changes significant state
- Stored in the project's local knowledge, not in public repos
- Format: see `templates/` in this repo

---

## Release Standards

### Pre-release checklist
See `SECURITY.md` — Pre-Release Security Checklist.
All items must be checked before any build is distributed.

### SDK versioning
See `conventions/versioning_policy.md`.
SDKs follow Semantic Versioning. AU projects pin by tag — never by branch.

### The M5 Gate
No commercial release until M5 Studio is acquired.
Final DSP optimisation, notarization, and Apple Silicon validation
occur on M5 hardware. This is non-negotiable.

---

## Related Documents

- `SECURITY.md` — standing security principles
- `AGENT_BOOTSTRAP.md` — agent session bootstrap reference
- `contracts/` — public API surface contracts
- `conventions/` — detailed convention references
- `templates/` — document and file templates

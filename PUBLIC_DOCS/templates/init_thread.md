# {PROJECT_NAME} — Thread Init
**Repo:** `temporaldsp-admin/{REPO_NAME}`
**Local path:** `{LOCAL_PATH}`
**Current stage:** {STAGE} — {PHASE}
**Status:** {ONE_LINE_STATUS}

---

## Governance Rules

1. Top-level `TemporalDSP/` is never a git repo
2. One project = one repo = one GitHub remote
3. SDKs are versioned Swift Packages — consumers pin by tag, never by branch
4. No git submodules — Swift Package Manager handles all SDK dependencies
5. SDK features must exist and be tested before product implementation
6. Rust reserved for legacy License Manager only — everything else is Swift
7. No commercial release until M5 Studio acquired and Apple Silicon validated
8. `STAGING/` is local only — never pushed
9. `Package.resolved` — never commit in SDK libraries, always commit in AU/App projects

---

## Shared Standards

All shared standards, contracts, and conventions:
**https://github.com/temporaldsp-admin/DOCS**

Fetch conditionally — only when your task requires it:

| Task type | Fetch |
|---|---|
| DSP implementation | `PUBLIC_DOCS/STANDARDS.md` |
| Public SDK API change | `PUBLIC_DOCS/contracts/TemporalDSPKit_public_api.md` |
| UI SDK API change | `PUBLIC_DOCS/contracts/TemporalDSPUI_public_api.md` |
| Security-sensitive change | `PUBLIC_DOCS/SECURITY.md` |
| Commit / branch / tag work | `PUBLIC_DOCS/conventions/git_conventions.md` |
| New Swift file / naming | `PUBLIC_DOCS/conventions/swift_conventions.md` |
| SDK version bump | `PUBLIC_DOCS/conventions/versioning_policy.md` |

Full bootstrap:
**https://raw.githubusercontent.com/temporaldsp-admin/DOCS/main/PUBLIC_DOCS/AGENT_BOOTSTRAP.md**

---

## This Project

{PROJECT_SPECIFIC_CONTEXT}

### What is built
{WHAT_IS_BUILT}

### What is not built yet
{WHAT_IS_NOT_BUILT}

### Before you write any code
{PRE_CODE_CHECKLIST}

---

## Session Protocol

1. Confirm stage and phase above match your task
2. Fetch conditional documents that apply to your task
3. One commit per phase — Conventional Commits format
4. All tests pass before committing to main
5. End of session: write handover note if mid-phase

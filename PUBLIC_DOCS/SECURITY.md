# TemporalDSP — Security
**Status:** Living document
**Owner:** Solo dev
**Last updated:** 2026-05-21

---

## Purpose

Front-door reference for security across the TemporalDSP ecosystem.
Captures standing principles. Points to detailed artefacts in component projects.

This document does not contain threat models, attack trees, or
implementation detail. Those live alongside the components they describe.

---

## Standing Principles

1. **Economic safety is a security property.**
   Architecture stays within free tiers. A DDoS or viral freebie
   cannot generate a cloud bill.

2. **Bounded online verification, not always-online.**
   Licensed products phone home on activation and on suspicious local
   state. Normal use is silent and offline.

3. **Local enforcement strength carries the load.**
   Apple platform primitives (Secure Enclave, App Attest, signed XPC)
   are used wherever available — free, strong, Apple-maintained.

4. **One language per trust boundary.**
   Swift for everything on the Apple side. No mixed-language trust
   boundaries in shipped products.

5. **SDK-first, product-second.**
   Security-critical code lives in a Swift Package testable in isolation.
   Products link it. Attack surface stays reviewable.

6. **Code signing and notarization are non-negotiable.**
   Every shipped binary is signed, notarized, Hardened Runtime enabled.
   XPC connections require code-signing matches.

7. **No commercial release until M5 Studio acquired.**
   Notarization drills and Apple Silicon validation happen on M5 hardware.

8. **Pen-test before designing the next layer.**
   New security designs follow real attack data from the prior product.

9. **Right-size the security budget.**
   Minimum viable posture for v1: online activation, periodic
   re-validation, hardware binding, signed XPC, redundant local checks.

10. **Supply chain hygiene is part of security.**
    Dependencies pinned by exact version or full commit SHA.
    `Package.resolved` committed in apps and AU projects, ignored in
    SDK libraries.

---

## Pre-Release Security Checklist

### Build Integrity
- [ ] Clean build from a fresh checkout
- [ ] All tests passing
- [ ] No debug symbols or build artefacts in repo
- [ ] No committed secrets, `.env` files, or API keys
- [ ] `Package.resolved` committed for apps, ignored for libraries

### Apple Gate
- [ ] Signed with correct Team ID
- [ ] Hardened Runtime enabled
- [ ] App Sandbox configured where applicable
- [ ] Notarized by Apple
- [ ] Gatekeeper passes on a clean machine

### License Integration
- [ ] XPC connection requires code-signing match
- [ ] Local license check runs at multiple code paths
- [ ] No license bypass via environment variable or debug flag
- [ ] Hardware binding uses Secure Enclave on Apple Silicon

### Supply Chain
- [ ] Dependencies pinned by exact version or SHA
- [ ] No new dependencies added since last audit
- [ ] No npm packages in Swift projects
- [ ] GitHub Actions pinned by full commit SHA

### Public Hosting
- [ ] SHA256 published alongside binary
- [ ] Storefront is static — no dynamic server attack surface
- [ ] Payment processor handles all card data

---

## Audit Cadence

| Cadence | Activity |
|---|---|
| Per release | Pre-release checklist above |
| Per new product beta | Pen-test before commercial release |
| Quarterly | Secrets sweep across all repos |
| Quarterly | Dependency audit |
| Annually | Threat model review per component |

---

## Component Security Documents

| Component | Location |
|---|---|
| License Manager (Swift) | Component repo DOCS/ — deferred until first AUv3 beta |
| TemporalDSPKit | SDK README |
| TemporalDSPUI | SDK README |

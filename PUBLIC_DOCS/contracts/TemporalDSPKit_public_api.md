# TemporalDSPKit — Public API Contract
**Status:** PENDING STUB AUDIT — not authoritative until status changes to LOCKED
**Last updated:** 2026-05-21
**Version:** pre-v0.1.0

---

## Purpose

Defines the public API surface of `TemporalDSPKit` that consumer
projects may depend on.

Any change to a symbol listed here:
- Requires a SemVer version bump (see `conventions/versioning_policy.md`)
- Requires an entry in `DOCS/API/surface_update.log` (local)
- Must not break pinned consumers without a coordinated update

---

## Status Note

Stub pending SDK stub audit. Audit identifies which modules are built
and tested vs placeholder. This file is populated after the audit
completes and SDKs are tagged v0.1.0.

**Do not treat anything here as stable until status is LOCKED.**

---

## Modules

| Module | Status |
|---|---|
| Dynamics | Built — Stage 07 complete |
| Filters | Built |
| Metering | Built |
| Saturation | Built |
| GainStaging | Built |
| LoudnessStandards | Built |
| Output | Built |
| Protocols | Built |
| Utilities | Built |
| Preamping | Planned — Stage 08 scope |
| Spatial | Planned |

Public symbols to be documented post-audit.

---

## Change Log

| Date | Version | Change |
|---|---|---|
| 2026-05-21 | pre-v0.1.0 | Stub created pending audit |

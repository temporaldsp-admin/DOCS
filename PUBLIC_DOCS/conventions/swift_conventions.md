# Swift Conventions
**Status:** Active
**Last updated:** 2026-05-21

---

## Reference Standard

All Swift code follows the **Apple Swift API Design Guidelines**:
https://swift.org/documentation/api-design-guidelines/

This document records TemporalDSP-specific additions and clarifications.

---

## Naming

### Types
- `PascalCase` for all types, protocols, enums
- Protocol names describe capability: `AudioProcessing`, not `AudioProcessor`
- Enum cases: `camelCase`

### Functions and methods
- `camelCase`
- Verb-first for mutating: `process(_:)`, `reset()`
- Noun-first for non-mutating: `gainReduction(for:)`

### DSP-specific suffixes
| Suffix | Use for | Example |
|---|---|---|
| `Db` | Gain in decibels | `makeupDb`, `thresholdDb` |
| `Ms` | Time in milliseconds | `attackMs`, `releaseMs` |
| `Hz` | Frequency in hertz | `sidechainHpfHz` |
| `Linear` | Linear gain (where ambiguous) | `gainLinear` |

- Sample rate: always `sampleRate` — never `fs` or `sr`
- Buffer: always `buffer` — never `buf`

---

## File Structure

```swift
// 1. Imports
// 2. Type declaration
//    3. Public properties
//    4. Private properties
//    5. Initialiser
//    6. Public methods
//    7. Private methods
```

---

## Documentation Comments

All public symbols require DocC documentation:

```swift
/// Summary line.
///
/// Extended description if needed.
///
/// - Parameters:
///   - inputLevel: Input level in dBFS
/// - Returns: Gain reduction in dB (positive = reduction applied)
public func computeGainReduction(inputLevel: Float) -> Float
```

---

## Tooling

- **SwiftLint** — config at `.swiftlint.yml` in each repo root
- **SwiftFormat** — config at `.swiftformat` in each repo root
- Warnings treated as errors on `main`
- Do not fight the formatter

---

## Testing Conventions

Every DSP component requires two test files:
```
{Component}CorrectnessTests.swift  — mathematical correctness
{Component}CharacterTests.swift    — sonic/perceptual character
```

Test function naming:
```swift
func test_{component}_{condition}_returns_{expected}()
```

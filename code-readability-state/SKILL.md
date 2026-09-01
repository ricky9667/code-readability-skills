---
name: code-readability-state
description: "Make state transitions explicit and robust."
---
# Code Readability: State

Readable state has a small domain, one source of truth, explicit transitions, and invariants that are difficult to violate. Do not add state for an imagined future feature.

## Procedure

- List each state value, owner, domain, and allowed transitions.
- Remove redundant state; derive values from their source of truth.
- Replace non-orthogonal flags with a function or sum type.
- Prefer immutable snapshots and narrow mutation ownership.
- Check illegal states, event ordering, repeated events, and cycles.
- Make naturally repeated operations idempotent.
- Validate external input at the boundary and use types for domains.
- Test valid/invalid transitions, repetition, and cycles.

## Examples

Avoid invalid combinations of flags:

```kotlin
var isLoading = false
var hasError = false
var data: Data? = null
```

Use a sum type:

```kotlin
sealed interface ScreenState {
    data object Loading : ScreenState
    data class Ready(val data: Data) : ScreenState
    data class Failed(val cause: Throwable) : ScreenState
}
```

Do not store derivable state:

```kotlin
val isExpired: Boolean get() = clock.now() >= expiresAt
```

Make transitions immutable and idempotent:

```kotlin
data class CartState(val items: List<Item>, val submitted: Boolean)
fun submit(s: CartState) = if (s.submitted) s else s.copy(submitted = true)
```

## Verification

- Owner and source of truth are clear.
- Invalid combinations are unrepresentable or rejected.
- Repeated events and ordering are tested.
- Derived state is not duplicated as mutable state.

Source: https://speakerdeck.com/munetoshi/code-readability-session-4-ver-2-en

---
name: code-readability-comments
description: "Write comments that explain intent without duplicating code."
---
# Code Readability: Comments

Comments should reduce uncertainty, prevent mistakes, or preserve knowledge code cannot express. If a comment is needed because code is poorly named or structured, improve the code first.

## Procedure

- Document observable behavior, preconditions, postconditions, errors, side effects, limitations, invariants, and reasons.
- Use documentation comments for APIs and types; use informal comments for overview, background, reason, or pitfalls.
- Do not repeat a symbol name, translate each line, mention private implementation details, or say who calls the function.
- Treat a long comment as a refactoring signal: rename, split parameters, simplify errors, or remove an unnecessary return value.
- Keep TODO/FIXME comments actionable and linked to a real task.
- Recheck comments after every refactor; stale comments are harmful.

## Examples

Explain why, not what:

```kotlin
// Copy explicitly so later writes cannot mutate the snapshot.
val listSnapshot = list.toList()
```

Refactor a long contract around an unclear API:

```kotlin
/** Adds or overwrites the definition for [keyword]. */
fun registerDefinition(keyword: String, definitionText: String)
```

Document observable behavior:

```kotlin
/**
 * Shows [photoData] centered when valid; returns false without changing the view otherwise.
 */
fun showPhotoView(photoData: PhotoData): Boolean { ... }
```

Explain a necessary surprising invariant:

```kotlin
// Publish on the main thread: observers render immediately.
stateStore.replace(snapshot)
```

## Verification

- Each comment answers a question code cannot answer.
- No comment merely translates code or repeats a name.
- TODOs are actionable and documentation matches behavior.

Source: https://speakerdeck.com/munetoshi/code-readability-session-3-ver-2-en

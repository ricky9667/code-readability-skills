---
name: code-readability-dependency-ii
description: "Keep dependencies acyclic, direct, and explicit."
---
# Code Readability: Dependency II

Prefer dependency graphs that are acyclic, direct where meaningful, and visible from definitions or diagrams. Preferred directions are caller→callee, concrete→abstract, complex→simple, mutable→immutable, unstable→stable, and algorithm→data model.

## Procedure

- Draw or inspect the graph; locate cycles, indirect references, and duplicated dependency sets.
- Restore caller→callee by passing values. For asynchronous work, extract a focused provider/promise/coroutine boundary.
- Remove downcasts and `this is` checks from base classes; override behavior in subtypes.
- Keep simple data models independent of lifecycle-heavy services.
- Flatten cascaded dependencies: do not access an unrelated object's dependency just to obtain a reference.
- Consolidate duplicated dependency sets only when a real intermediate boundary is needed.
- Use subtyping for polymorphism, sum types, dependency inversion, or module separation—not just code sharing.
- Replace implicit primitive domains with model types or enums.

## Examples

Pass a value instead of making a view call back into a presenter:

```kotlin
videoPlayerView.play(presenter.getVideoUri())
fun play(videoUri: Uri) { ... }
```

Replace base-class downcasts with overriding:

```kotlin
open class IntList { open fun addElement(value: Int) { ... } }
class ArrayIntList : IntList() {
    override fun addElement(value: Int) { ... }
}
```

Make a hidden string domain explicit:

```kotlin
enum class BackgroundColor(val code: Int) { RED(0xFF0000), GREEN(0x00FF00) }
fun setViewBackgroundColor(color: BackgroundColor) { view.setBackgroundColor(color.code) }
```

## Verification

- No accidental dependency cycles remain.
- Call direction and ownership are visible.
- No unrelated transitive reference or unjustified abstraction remains.
- Domains are represented by types or boundary validation.

Source: https://speakerdeck.com/munetoshi/code-readability-session-7-ver-2-en

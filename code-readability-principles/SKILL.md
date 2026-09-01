---
name: code-readability-principles
description: "Improve code readability with foundational principles."
---
# Code Readability: Introduction and Principles

Use this when changing code and deciding whether to refactor, abstract, or optimize. Readability means code is obvious, simple, isolated, and structured; at scale, reading and reviewing code dominates initial writing time.

## Procedure

- Trace responsibility, state transitions, dependencies, and callers before editing.
- Apply the boy scout rule: improve code when touching it, but do not add to a huge class, function, layer, or call hierarchy. Refactor first or make a small separate change.
- Apply YAGNI: remove unused symbols, commented-out code, speculative parameters, and one-implementation abstractions.
- Apply KISS: prefer standard mechanisms and named intermediate values over clever chains.
- Keep each class responsibility explainable in one short sentence; split when its summary is ambiguous or too long.
- Optimize only after profiling or estimating value, and prefer optimizations that simplify code.
- Run compiler, formatter, tests, and static checks.

## Examples

Refactor before adding another branch:

```kotlin
enum class ViewType(val isView1Visible: Boolean, val view2Text: String) {
    A(true, "Case A"), B(false, "Case B"), Z(true, "Case Z")
}
view1.isVisible = viewType.isView1Visible
view2.text = viewType.view2Text
```

Prefer named stages to a clever chain:

```kotlin
val logCountByUser = logs.groupBy { log -> log.user }
    .map { (user, userLogs) -> user to userLogs.size }
val usersSortedByLogCount = logCountByUser.sortedBy { (_, count) -> count }
    .map { (user, _) -> user }
return usersSortedByLogCount.takeLast(10)
```

Keep responsibilities separate:

```kotlin
data class BookData(val id: Int, val name: String)
data class UserData(val name: String)
class CirculationRecord { data class Entry(val renter: UserData, val dueDate: LocalDate) }
```

A lookup can be simpler and faster:

```kotlin
val data = map[expectedKey] // rather than list.find { it.key == expectedKey }
```

## Verification

- Every new element serves a current requirement.
- Responsibility and scope are clear.
- No speculative API or abstraction was added.
- Tests and automatic checks pass.

Source: https://speakerdeck.com/munetoshi/code-readability-session-1-ver-2-en

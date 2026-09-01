---
name: code-readability-function
description: "Design functions with one clear purpose and flow."
---
# Code Readability: Function

A readable function has a clear responsibility, explicit inputs/outputs, visible side effects, and a scan-friendly control flow. Small size alone is not the goal.

## Procedure

- State the responsibility in one sentence and compare it with the name.
- Keep inputs minimal; do not pass caller context when behavior can be expressed directly.
- Separate querying from mutation when practical; expose side effects and return values.
- Use guard clauses for invalid input and errors.
- Extract only distinct, named, independently testable responsibilities.
- If a function mutates and returns a value, document the contract or redesign it.
- Test normal, boundary, error, and repeated-call behavior.

## Examples

Name behavior, not screen context:

```kotlin
fun showHistory(shouldShowDialogOnError: Boolean) // behavior
// rather than isCalledAtMainScreen: caller detail
```

Return success and let callers choose presentation:

```kotlin
fun showPhotoView(data: PhotoData): Boolean {
    if (!data.isValid) return false
    photoView.showCentered(data)
    return true
}
if (!showPhotoView(data)) showErrorDialog()
```

Keep orchestration and focused work visible:

```kotlin
fun updateProfile(p: Profile) {
    updateName(p.name)
    updateBirthday(p.birthday)
    updateImage(p.imageUrl)
}
```

## Verification

- Name, parameters, return value, and side effects tell the same story.
- Callers do not need hidden callback tracing.
- Extraction reduced responsibility rather than scattering it.
- Edge, error, and idempotence tests pass where relevant.

Source: https://speakerdeck.com/munetoshi/code-readability-session-5-ver-2-en

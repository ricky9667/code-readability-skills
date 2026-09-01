---
name: code-readability-dependency-i
description: "Reduce harmful coupling between collaborating components."
---
# Code Readability: Dependency I

Coupling is how components depend on one another. Prefer meaningful data or message coupling, but do not add abstraction merely to appear decoupled: implicit dependencies can be harder to understand.

## Procedure

- Identify dependencies on internals, mutable globals, control flags, whole structures, data, or messages.
- Replace content coupling with public behavior.
- Narrow common/external mutable state and make lifecycle ownership explicit.
- Split control-coupled functions by object when targets differ; split functions when the condition selects a static behavior; otherwise consider a constrained strategy.
- Choose stamp coupling deliberately: a data object may preserve meaning and type safety.
- Use data coupling only when same-typed positional values cannot be confused.
- Keep feature-specific logic out of widely reused model classes.

## Examples

Split a large conditional by target:

```kotlin
fun updateUserNameView() { userNameView.text = getUserName() }
fun updateBirthdayView() { birthdayView.text = format(getBirthday()) }
fun updateProfileImage() { profileImage.load(getImageUrl()) }
```

A typed object can be safer than two strings:

```kotlin
fun updateUserView(user: UserData) {
    userNameView.text = user.fullName
    profileImage.setImageUrl(user.profileImageUrl)
}
// updateUserView(imageUrl, fullName) compiles but swaps meaning
```

A parameterless command such as idempotent `close()` can be message coupling; still check whether it hides shared internals.

## Verification

- Every dependency has an owner and reason.
- No component reaches through another's internals.
- Control flags do not hide unrelated responsibilities.
- Same-typed parameters are safe or wrapped in a domain type.

Source: https://speakerdeck.com/munetoshi/code-readability-session-6-ver-2-en

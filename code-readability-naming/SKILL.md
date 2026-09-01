---
name: code-readability-naming
description: "Choose accurate and unambiguous names for code."
---
# Code Readability: Naming

Name things so a reader understands what they are or do without tracing who called them, when they are called, or how they work.

## Procedure

- Use accurate, descriptive names: `isVisible`, `width`, `imageUrl`, not `flag`, `w`, or `image`.
- Match grammar to kind: nouns for types/values, imperatives for functions, adjectives for state, interrogative verbs for booleans, and prepositional phrases for converters.
- Put the essential word at the end: `MessageEventHandler`, `buttonHeight`; use `getX`, `postY`, `mapToZ` for actions.
- Describe what, not caller context: use `storeReceivedMessage` rather than `onMessageReceived` when storing is the behavior.
- Replace ambiguous words: `shouldInitialize`, `isInitializing`, `wasInitialized`; `maxHeight` or `maxBytes` rather than `sizeLimit`.
- Avoid private abbreviations. URL/TCP are common; product abbreviations need a glossary.
- Add units/entities: `timeoutInMillis`, `widthInPixels`, `colorResId`, `userIndex`.
- Prefer positive names: `isEnabled`, not `isNotDisabled`.

## Examples

```kotlin
class MessageEventHandler
val buttonHeight: Int
fun findMessage(id: MessageId): Message
fun shouldShowDialog(): Boolean
fun toInt(value: String): Int
```

Caller-context is fragile:

```kotlin
fun showHistory(shouldShowDialogOnError: Boolean) // behavior
fun showHistory(isCalledAtMainScreen: Boolean)   // temporary caller detail
```

Make units type-safe when mistakes matter:

```kotlin
class Inch(val value: Int)
class Centimeter(val value: Int)
fun setWidth(width: Inch) = Unit
// setWidth(Centimeter(10)) // compile-time error
```

## Verification

- A reader can state what every changed symbol is or does.
- Grammar, polarity, units, and domain are explicit.
- Names do not encode obsolete caller history.
- Project conventions are followed and related call sites are updated.

Source: https://speakerdeck.com/munetoshi/code-readability-session-2-ver-2-en

---
name: code-readability-review
description: "Prepare focused reviews and give intent-aware feedback."
---

# Code Readability: Review

Review readability from another engineer's perspective and check correctness risks the author may miss. Review the code and specification, not the person's character. Redirect huge or fundamentally misguided changes before line-by-line review.

## Author procedure

- Describe purpose, expected result, out-of-scope work, and future plan.
- Keep the pull request small. Split large features top-down with skeleton structure or bottom-up with independent parts.
- Finish additional refactoring first or restructure commits; do not bundle unrelated work.
- Understand the intent of every comment, diagnose the misunderstanding, and search for similar code.

## Reviewer procedure

- Be respectful and efficient; use questions and evidence.
- Check scope, naming, comments, state, functions, dependencies, tests, edge cases, errors, races, security, performance, and footprint.
- Reject or resize changes whose purpose or structure is critically wrong instead of spending unlimited review time.
- Never lower the approval threshold only because of a deadline; record tests and follow-up agreements for exceptions.
- If unavailable, give a realistic response time or redirect; never promise and silently fail.

## Examples

Split work into reviewable pieces:

```kotlin
class UserProfilePresenter(private val useCase: UseCase, private val rootView: View) {
    fun showProfileImage() = TODO("implement in a later change")
}
```

Avoid caller-context coupling:

```kotlin
fun showPhotoView(data: PhotoData): Boolean { ... }
```

A useful comment explains the reason and asks for a reusable fix:

> The boolean selects error UI inside a reusable photo function. Could it return success/failure and let each caller choose presentation? Please check other callers for the same coupling.

## Verification

- The description and diff have one responsibility.
- Commits can be reviewed independently.
- Comments are actionable and intent-aware.
- Readability and correctness risks were checked without personal judgment.
- Tests and automatic checks pass; unresolved risks are explicit.

Source: https://speakerdeck.com/munetoshi/code-readability-session-8-ver-2-en

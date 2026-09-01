# Code readability skills

Agent skills for reviewing and improving code readability. They cover principles, naming, comments, state, functions, dependencies, and code review.

The skills adapt Munetoshi's [Code Readability presentations](https://gist.github.com/munetoshi/65a1b563fb2c271f328c121a4ac63571) into concise instructions that coding agents can apply while working on a codebase.

## Installation

Clone the repository:

```sh
git clone https://github.com/ricky9667/code-readability-skills.git
```

Copy every `code-readability-*` directory into the user-level or project-level skills directory used by your coding agent:

```sh
cp -R code-readability-skills/code-readability-* /path/to/your-agent/skills/
```

The exact destination depends on the agent. These skills work with coding agents that support the `SKILL.md` format. You can copy a single directory if you only need one skill. Start a new agent session after installation so the skills are discovered.

## Reference

| Skill | Focus |
| --- | --- |
| [`code-readability-principles`](code-readability-principles/SKILL.md) | Foundational readability principles |
| [`code-readability-naming`](code-readability-naming/SKILL.md) | Accurate and unambiguous names |
| [`code-readability-comments`](code-readability-comments/SKILL.md) | Comments that explain intent |
| [`code-readability-state`](code-readability-state/SKILL.md) | Explicit state and valid transitions |
| [`code-readability-function`](code-readability-function/SKILL.md) | Focused functions with clear flow |
| [`code-readability-dependency-i`](code-readability-dependency-i/SKILL.md) | Coupling between components |
| [`code-readability-dependency-ii`](code-readability-dependency-ii/SKILL.md) | Dependency direction and cycles |
| [`code-readability-review`](code-readability-review/SKILL.md) | Focused, intent-aware code reviews |

Each skill links to its corresponding English presentation. The [original source index](https://gist.github.com/munetoshi/65a1b563fb2c271f328c121a4ac63571) also includes the Japanese presentations and related material.

## License

This repository is available under the [MIT License](LICENSE). The original presentation material belongs to its respective author and remains subject to its own terms.

# Dev Prompts

Reusable prompts, guidelines, and AI-assisted software development workflows.

This repository provides a versioned and documented collection of reusable AI instructions for software engineering.

The goal is to maintain a small, reliable library of prompts that can be reused across projects without mixing unrelated project context.

## Purpose

This repository exists to:

- maintain reusable prompts in a single source of truth;
- version prompt evolution with Git;
- make prompts discoverable and documented;
- avoid duplicating prompts across projects;
- support reusable development workflows;
- separate generic AI instructions from project-specific context;
- expose only relevant prompts to each project.

Prompts in this repository are treated as software artifacts.

They should evolve through real usage, testing, review, and version control.

## Repository Structure

```text
dev-prompts/
├── README.md
├── CONTRIBUTING.md
│
├── guidelines/
│   └── .gitkeep
│
└── prompts/
    ├── architecture/
    │   └── .gitkeep
    │
    ├── bug-fixing/
    │   └── .gitkeep
    │
    ├── testing/
    │   └── .gitkeep
    │
    └── utils/
        └── code-review/
            ├── README.md
            └── prompt.md
```

The structure evolves from real usage.

New categories should only be introduced when reusable prompts actually require them.

## Prompt Catalog

### Utilities

| Prompt | Purpose | Documentation | Prompt |
| --- | --- | --- | --- |
| Code Review | Review focused code changes and identify concrete engineering risks. | [Documentation](./prompts/utils/code-review/README.md) | [Prompt](./prompts/utils/code-review/prompt.md) |

More prompts will be added as reusable workflows emerge from real development needs.

## Prompt Folder Convention

Each reusable prompt should normally have its own directory:

```text
prompt-name/
├── README.md
└── prompt.md
```

### `prompt.md`

The canonical prompt.

It contains the instructions consumed by a developer or AI tool.

### `README.md`

Human-facing documentation.

It should explain things such as:

- objective;
- when to use the prompt;
- when not to use it;
- expected inputs;
- expected outputs;
- project-context requirements;
- tested models;
- known limitations;
- evaluation status;
- recent behavioral changes.

The prompt and its documentation have different responsibilities:

```text
prompt.md
→ how the AI should behave

README.md
→ how humans should understand and use the prompt
```

## Reusable vs. Project-Specific

A reusable prompt belongs in this repository when it can reasonably be applied across multiple projects.

A useful question is:

> Would this prompt still make sense, mostly unchanged, in another project?

If the answer is **yes**, it is probably reusable.

Examples:

```text
code review
bug investigation
test generation
architecture analysis
commit generation
pull request preparation
```

Project-specific instructions should remain in the repository that owns that context.

Examples:

```text
AGENTS.md
CLAUDE.md
project-specific commands
project workflows
domain rules
architecture constraints
testing conventions
repository-specific guidelines
```

For example:

### Reusable

```text
Review the provided Git diff and identify concrete bugs,
regressions, security problems, and missing tests.
```

### Project-Specific

```text
Controllers in this project must never access Prisma directly.
All persistence must go through repositories.
```

The first belongs here.

The second belongs in the project that follows that architecture.

## Composition

Reusable prompts are designed to be combined with more specific context.

Conceptually:

```text
reusable task prompt
        +
technical specialization
        +
project instructions
        +
current task input
        =
contextualized execution
```

For example:

```text
generic code-review prompt
        +
AGENTS.md
        +
current Git diff
        =
project-aware code review
```

This allows the reusable prompt to remain generic while the target project provides its own rules.

## Using Prompts in a Project

Projects should not copy this entire repository into their codebase.

Only expose the reusable prompts required by the current project.

A recommended local structure is:

```text
my-project/
├── .prompts/
│   └── code-review.md
│
├── AGENTS.md
├── src/
└── ...
```

The local file can be a symbolic link to the canonical prompt stored here.

Example:

```text
my-project/.prompts/code-review.md
        │
        └──> dev-prompts/prompts/utils/code-review/prompt.md
```

This provides:

- one canonical prompt;
- no manual duplication;
- automatic access to local updates;
- less unrelated context inside the target project.

## Symbolic Links

Example on Windows:

```text
C:\Users\<user>\dev-prompts\
└── prompts\
    └── utils\
        └── code-review\
            └── prompt.md
```

A project may expose that prompt as:

```text
project\.prompts\code-review.md
```

while the canonical file remains inside this repository.

The target project should normally ignore local reusable prompt links:

```gitignore
# Local reusable prompts
.prompts/
```

This prevents machine-specific symbolic links from being committed accidentally.

Project-owned prompts should still be versioned normally inside their own repository.

## Why Not Expose Everything?

AI coding tools may inspect files available inside the project context.

Exposing the entire prompt library can introduce:

- irrelevant instructions;
- conflicting guidelines;
- unnecessary context;
- increased token usage;
- ambiguous agent behavior.

For example, a Next.js project should not automatically expose unrelated:

```text
Go guidelines
Python instructions
Laravel conventions
infrastructure prompts
workflows from another project
```

More context is not automatically better context.

Expose only what is useful for the current task.

## Categories

The repository may eventually contain categories such as:

### Exploration & Planning

Prompts used before implementation.

Examples:

- codebase exploration;
- dependency analysis;
- security exploration;
- feature planning;
- modernization analysis.

### Documentation

Prompts for creating or maintaining:

- ADRs;
- RFCs;
- PRDs;
- design documents;
- technical documentation.

### Implementation

Prompts that participate directly in software changes.

Examples:

- bug fixing;
- test generation;
- refactoring;
- development workflows.

### Infrastructure

Prompts related to:

- Docker;
- Docker Compose;
- Kubernetes;
- Terraform;
- CI/CD.

### Utilities

Frequently used development operations.

Examples:

- code review;
- commit generation;
- pull request preparation.

### Specializations

Reusable technical context that complements task prompts.

Examples:

```text
languages/
frameworks/
testing/
infrastructure/
```

A generic task prompt and a specialization may be composed instead of duplicating the entire task prompt for every technology.

For example:

```text
generic testing prompt
        +
Go testing guidelines
        =
Go-specific testing behavior
```

Categories are created only when real reusable artifacts justify them.

## Versioning

Git is the source of truth for prompt history.

Do not create informal versions such as:

```text
prompt-final.md
prompt-v2.md
prompt-new.md
prompt-best.md
prompt-final-final.md
```

Keep one canonical prompt and represent its evolution through commits.

For example:

```text
prompts/utils/code-review/prompt.md
```

Its history belongs in Git.

Prompt-level documentation may contain a small human-readable changelog for important recent behavioral changes.

## Contributing

Contribution rules, prompt design conventions, testing guidance, versioning workflow, commit conventions, and review practices are documented in:

[CONTRIBUTING.md](./CONTRIBUTING.md)

Before adding or modifying a reusable prompt, review those guidelines.

## Public Repository

This repository is public.

Do not commit:

- credentials;
- API keys;
- tokens;
- private URLs;
- customer data;
- confidential business rules;
- proprietary source code;
- sensitive infrastructure information;
- prompts owned by clients or employers.

Project-specific or confidential instructions belong in the appropriate private repository.

## Current Prompts

### Code Review

Perform focused, evidence-based code reviews that prioritize concrete engineering risks over stylistic preferences and speculative findings.

- [Documentation](./prompts/utils/code-review/README.md)
- [Prompt](./prompts/utils/code-review/prompt.md)

## Principles

This repository follows a few simple principles:

```text
one canonical source
        ↓
Git versioning
        ↓
human documentation
        ↓
selective project exposure
        ↓
real usage
        ↓
evaluation and improvement
```

The objective is not to build the largest possible prompt collection.

The objective is to maintain reusable AI instructions that demonstrably improve software-development workflows.
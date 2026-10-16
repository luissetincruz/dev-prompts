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
    ├── documentation/
    │   ├── feature-prd/
    │   │   ├── README.md
    │   │   └── prompt.md
    │   │
    │   ├── high-level-design/
    │   │   ├── README.md
    │   │   └── prompt.md
    │   │
    │   └── feature-design/
    │       ├── README.md
    │       └── prompt.md
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

### Documentation

| Prompt | Purpose | Documentation | Prompt |
| --- | --- | --- | --- |
| Feature PRD | Conduct a structured requirements interview and generate a feature-level Product Requirements Document. | [Documentation](./prompts/documentation/feature-prd/README.md) | [Prompt](./prompts/documentation/feature-prd/prompt.md) |
| High-Level Design | Define a context-aware system architecture and generate a High-Level Design with explicit decisions, risks, interfaces, and open questions. | [Documentation](./prompts/documentation/high-level-design/README.md) | [Prompt](./prompts/documentation/high-level-design/prompt.md) |
| Feature Design | Define detailed feature behavior, public contracts, failure semantics, compatibility, observability, and technical acceptance criteria. | [Documentation](./prompts/documentation/feature-design/README.md) | [Prompt](./prompts/documentation/feature-design/prompt.md) |

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
feature PRD generation
high-level design generation
feature design generation
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

Or:

```text
generic feature-PRD prompt
        +
project documentation
        +
existing ADRs
        +
feature context
        =
project-aware Feature PRD
```

Or:

```text
generic high-level-design prompt
        +
Feature PRD
        +
existing architecture
        +
ADRs / RFCs
        +
technical research
        +
codebase context
        =
project-aware High-Level Design
```

Or:

```text
generic feature-design prompt
        +
Feature PRD
        +
High-Level Design
        +
ADRs / RFCs
        +
technical research
        +
existing contracts
        +
codebase and tests
        =
project-aware Feature Design Doc
```

This allows the reusable prompt to remain generic while the target project provides its own rules.

## Using Prompts in a Project

Projects should not copy this entire repository into their codebase.

Only expose the reusable prompts required by the current project.

A recommended local structure is:

```text
my-project/
├── .prompts/
│   ├── code-review.md
│   ├── feature-prd.md
│   ├── high-level-design.md
│   └── feature-design.md
│
├── AGENTS.md
├── src/
└── ...
```

The local files can be symbolic links to the canonical prompts stored here.

Examples:

```text
my-project/.prompts/code-review.md
        │
        └──> dev-prompts/prompts/utils/code-review/prompt.md
```

```text
my-project/.prompts/feature-prd.md
        │
        └──> dev-prompts/prompts/documentation/feature-prd/prompt.md
```

```text
my-project/.prompts/high-level-design.md
        │
        └──> dev-prompts/prompts/documentation/high-level-design/prompt.md
```

```text
my-project/.prompts/feature-design.md
        │
        └──> dev-prompts/prompts/documentation/feature-design/prompt.md
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
    ├── documentation\
    │   ├── feature-prd\
    │   │   └── prompt.md
    │   │
    │   ├── high-level-design\
    │   │   └── prompt.md
    │   │
    │   └── feature-design\
    │       └── prompt.md
    │
    └── utils\
        └── code-review\
            └── prompt.md
```

A project may expose only the prompts it needs, for example:

```text
project\.prompts\code-review.md
project\.prompts\feature-prd.md
project\.prompts\high-level-design.md
project\.prompts\feature-design.md
```

while the canonical files remain inside this repository.

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

or:

```text
prompts/documentation/feature-prd/prompt.md
```

or:

```text
prompts/documentation/high-level-design/prompt.md
```

or:

```text
prompts/documentation/feature-design/prompt.md
```

Their history belongs in Git.

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

### Feature PRD

Conduct an interview-driven requirements-elicitation workflow to create a clear, structured, and actionable Feature Product Requirements Document.

The prompt:

- reuses existing project context before asking questions;
- distinguishes confirmed information from hypotheses and unknowns;
- avoids inventing requirements or technical decisions;
- defines goals, scope, functional requirements, non-functional requirements, dependencies, risks, and acceptance criteria;
- performs consistency checks before generating the final document;
- produces a Markdown PRD with optional structured JSON output;
- preserves the boundary between feature requirements and detailed technical design.

- [Documentation](./prompts/documentation/feature-prd/README.md)
- [Prompt](./prompts/documentation/feature-prd/prompt.md)

### High-Level Design

Conduct a context-first architectural-design workflow to create a clear, structured, and reusable High-Level Design.

The prompt:

- reuses PRDs, architecture documentation, ADRs, RFCs, technical research, and codebase context before asking questions;
- asks one primary question at a time;
- requires confirmation after every architectural interview stage;
- distinguishes confirmed information, hypotheses, and unknowns;
- classifies architectural choices as existing constraints, confirmed decisions, proposed options, or open decisions;
- avoids inventing technologies, architectural patterns, or numeric quality targets;
- defines major components, responsibilities, request and data flows, high-level data ownership, and externally relevant interfaces;
- covers scalability, availability, resilience, security, observability, and architectural risks when relevant;
- preserves ADRs, RFCs, open questions, pending decisions, and references;
- performs consistency checks before generating the final document;
- preserves the boundary between HLD and lower-level Feature Design / implementation detail;
- produces a Markdown HLD with optional structured JSON output.

- [Documentation](./prompts/documentation/high-level-design/README.md)
- [Prompt](./prompts/documentation/high-level-design/prompt.md)

### Feature Design

Conduct a context-first feature-design workflow to create a technically actionable and traceable Feature Design Doc.

The prompt:

- reuses Feature PRDs, HLDs, ADRs, RFCs, technical research, existing contracts, codebase context, and tests before asking questions;
- asks one primary question at a time;
- requires confirmation after every feature-design interview stage;
- distinguishes confirmed information, hypotheses, and unknowns;
- uses stable IDs for objectives, flows, contracts, errors, observability, dependencies, acceptance criteria, risks, and hypotheses;
- avoids inventing endpoints, payloads, retries, timeouts, status codes, dependency versions, or numeric targets;
- defines detailed runtime flows and externally relevant contracts;
- classifies contracts as existing, new, modified, deprecated, removed, or proposed;
- defines error, exception, fallback, and resilience behavior;
- covers observability, dependencies, compatibility, migrations, and rollout constraints when relevant;
- connects technical acceptance criteria to flows, contracts, errors, and objectives;
- preserves upstream PRD, HLD, ADR, and RFC decisions while surfacing contradictions;
- distinguishes current code or test behavior from desired target behavior;
- performs consistency checks before generating the final document;
- preserves the boundary between Feature Design and lower-level implementation detail;
- produces a Markdown FDD with optional structured JSON output.

- [Documentation](./prompts/documentation/feature-design/README.md)
- [Prompt](./prompts/documentation/feature-design/prompt.md)

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
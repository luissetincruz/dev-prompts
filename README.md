# Dev Prompts

Central repository for reusable prompts, guidelines, and AI-assisted software development workflows.

## Purpose

This repository stores generic prompts, guidelines, and reusable AI workflows that can be shared across different software projects.

The main goals are to:

- keep reusable prompts in a single source of truth;
- version prompts using Git;
- avoid duplicating prompts across multiple projects;
- make prompt evolution traceable;
- allow prompts to be reviewed and improved over time;
- expose only the prompts that are relevant to each project;
- reduce context ambiguity for AI coding agents.

Project-specific instructions should remain inside the repository of the project they belong to.

## Principles

Prompts in this repository should be treated as software artifacts.

This means they should be:

- versioned;
- reviewable;
- testable;
- reusable;
- documented;
- incrementally improved;
- scoped to a clear purpose.

A prompt should not be added simply because it may be useful someday.

Reusable prompts should solve a recurring problem that can reasonably appear across multiple projects.

## Repository Structure

```text
dev-prompts/
├── README.md
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
    ├── code-review/
    │   └── code-review.md
    │
    └── testing/
        └── .gitkeep
```

The structure can evolve as new reusable prompt categories emerge.

Avoid creating categories prematurely.

## Prompt Categories

### Architecture

Reusable prompts related to:

- architecture analysis;
- architectural trade-offs;
- dependency analysis;
- system exploration;
- technical design;
- modernization analysis.

Example:

```text
prompts/architecture/
```

### Bug Fixing

Reusable prompts related to:

- bug investigation;
- root cause analysis;
- debugging workflows;
- minimal corrective changes;
- regression analysis.

Example:

```text
prompts/bug-fixing/
```

### Code Review

Reusable prompts used to review:

- pull requests;
- Git diffs;
- source code;
- regressions;
- security risks;
- maintainability issues;
- test coverage.

Example:

```text
prompts/code-review/code-review.md
```

### Testing

Reusable prompts related to:

- unit tests;
- integration tests;
- E2E tests;
- test-case discovery;
- missing test scenarios;
- regression tests.

Example:

```text
prompts/testing/
```

### Guidelines

Reusable guidelines that can complement prompts across multiple projects.

Examples include:

- general coding-agent behavior;
- minimal-change policies;
- code-review principles;
- debugging rules;
- prompt authoring conventions.

Example:

```text
guidelines/
```

## Organization Rules

### General Prompts

Reusable prompts that are not tied to a specific codebase belong in this repository.

Examples:

- code review;
- bug investigation;
- test generation;
- architecture analysis;
- dependency analysis;
- generic development workflows.

A general prompt should avoid assumptions about a specific:

- company;
- product;
- repository;
- architecture;
- domain;
- framework version;
- business rule.

For example, a generic code-review prompt may define how a code review should be performed, but it should not assume that every project uses Next.js, NestJS, PostgreSQL, or any other specific technology.

Technology-specific prompts may still exist when the technology itself is the reusable context.

For example:

```text
prompts/testing/jest.md
prompts/architecture/nestjs-analysis.md
```

if they become useful across multiple projects.

## Project-Specific Prompts

Prompts that depend on the architecture, conventions, domain rules, workflows, or technical decisions of a specific project should live inside that project's repository.

Examples:

- `AGENTS.md`;
- project-specific coding guidelines;
- project-specific commands;
- project-specific workflows;
- architectural constraints;
- domain rules;
- project-specific testing conventions;
- project-specific agent instructions.

For example:

```text
my-project/
├── AGENTS.md
├── CLAUDE.md
├── src/
└── ...
```

These files should be versioned together with the project because changes to them may change how AI agents interact with that codebase.

## General vs Project-Specific

A useful rule when deciding where a prompt belongs is:

> Would this prompt still make sense, mostly unchanged, in another project?

If the answer is **yes**, it is probably a reusable prompt and belongs in this repository.

If the answer is **no**, because it depends on project architecture, business rules, conventions, or internal decisions, it should probably live in the project's own repository.

Example:

### General

```text
Review the provided Git diff and identify concrete bugs,
regressions, security problems, and missing tests.
```

This can be reused across many projects.

### Project-Specific

```text
Controllers in this project must never access Prisma directly.
All persistence must go through repositories.
```

This belongs to the project that follows that architecture.

## Usage

Projects should **not** copy the entire contents of this repository.

A project should expose only the prompts required for its current workflow.

This prevents AI tools from reading unrelated instructions and reduces the risk of conflicting context.

For example, a Next.js project should not accidentally expose:

- Go guidelines;
- Python prompts;
- unrelated architecture rules;
- prompts created for another project.

Too many unrelated instructions may increase ambiguity instead of improving the AI's behavior.

## Local `.prompts` Directory

A project may create a local `.prompts` directory containing symbolic links to selected prompts from this repository.

Example:

```text
my-project/
├── .prompts/
│   ├── code-review.md
│   └── bug-fixing.md
│
├── AGENTS.md
├── src/
└── ...
```

The files inside `.prompts` may point to the real files stored in `dev-prompts`.

Conceptually:

```text
my-project/.prompts/code-review.md
        │
        └──> dev-prompts/prompts/code-review/code-review.md
```

This keeps a single source of truth while allowing each project to expose only the prompts it actually needs.

## Symbolic Links

The preferred local workflow is:

```text
dev-prompts
    │
    │ reusable source
    │
    └──────────────┐
                   │ symbolic link
                   ↓
            project/.prompts/
```

Do not duplicate the prompt manually unless there is a specific reason to create a project-specific variation.

If the reusable prompt evolves, projects using a symbolic link automatically reference the updated file.

## Git Ignore

When `.prompts` contains only local symbolic links to this external repository, it should normally be ignored by the project Git repository.

Example:

```gitignore
# Local reusable prompts
.prompts/
```

This prevents machine-specific symbolic-link paths from being committed accidentally.

This rule does **not** apply to prompts that belong to the project itself.

Project-specific files such as:

```text
AGENTS.md
CLAUDE.md
project commands
project workflows
```

should normally be versioned with that project.

## Prompt Versioning

Prompts are treated as software artifacts.

Every meaningful change should be recorded with Git.

Examples of changes that should normally be versioned include:

- changing agent behavior;
- adding or removing constraints;
- changing output format;
- adding evaluation criteria;
- changing scope;
- adding examples;
- modifying negative instructions;
- changing workflow steps;
- fixing ambiguous instructions.

Git provides:

- history;
- diffs;
- authorship;
- rollback;
- branches;
- pull requests;
- review.

## Commit Examples

Examples of useful prompt-related commits:

```text
feat: add general code review prompt
```

```text
feat: add reusable bug investigation prompt
```

```text
fix: prevent code review prompt from suggesting unrelated refactors
```

```text
refactor: simplify architecture analysis prompt
```

```text
docs: document reusable prompt workflow
```

Commit messages should describe the behavioral change being introduced whenever possible.

## Team Workflow

When prompts are shared by a team, changes should follow a collaborative workflow similar to source code.

Recommended flow:

```text
identify problem
      ↓
modify prompt
      ↓
test new behavior
      ↓
commit changes
      ↓
open pull request
      ↓
team review
      ↓
additional testing
      ↓
merge
```

A pull request for a prompt should ideally explain:

- what problem was observed;
- what changed in the prompt;
- what behavior is expected to improve;
- how the new version was tested;
- whether any trade-offs were introduced.

## Personal Workflow

For prompts used only by one developer, pull requests and formal code review are optional.

Git versioning is still recommended because it provides:

- history;
- rollback;
- experimentation;
- comparison between versions;
- protection against losing a useful prompt.

The workflow can be as simple as:

```text
edit
↓
test
↓
commit
↓
reuse
```

## Prompt Evolution

Prompts should be considered evolutionary artifacts.

A common lifecycle is:

```text
initial prompt
      ↓
real usage
      ↓
undesired behavior
      ↓
diagnosis
      ↓
prompt adjustment
      ↓
testing
      ↓
new version
```

For example:

```text
Problem:
The coding agent performs unrelated refactors while fixing bugs.

Prompt change:
Add an explicit minimal-change policy and negative instructions.

Expected result:
Bug fixes remain focused on the reported problem.
```

Repeated problems can eventually become reusable guidelines.

## Model Considerations

The same prompt may behave differently across different LLMs or different versions of the same model.

When a prompt is particularly important, consider recording which model or environment was used during validation.

For example:

```text
Prompt:
code-review.md

Validated with:
- Model A
- Model B

Observed differences:
- Model A follows severity classification more consistently.
- Model B produces more speculative findings.
```

Model-specific behavior should normally be documented rather than silently encoded into a supposedly generic prompt.

## Prompt Design Guidelines

Reusable prompts should favor:

- clear objectives;
- explicit scope;
- minimal necessary context;
- structured inputs;
- explicit output formats when useful;
- quality criteria;
- ambiguity handling;
- negative instructions when necessary;
- error handling when applicable.

Complex prompts may also define an explicit workflow.

Avoid adding sections merely because a template contains them.

Every instruction should serve a clear purpose.

## Avoid Prompt Bloat

More instructions do not automatically create a better prompt.

Excessive instructions may:

- increase token usage;
- increase ambiguity;
- create contradictory rules;
- make maintenance harder;
- reduce portability between models.

Prefer the smallest prompt that reliably produces the required behavior.

## Source of Truth

Reusable prompts stored in this repository should have one canonical file.

Avoid maintaining manually copied versions such as:

```text
code-review-final.md
code-review-new.md
code-review-final-v2.md
code-review-best.md
code-review-last.md
```

Use Git history instead.

The canonical file should remain:

```text
prompts/code-review/code-review.md
```

Its evolution should be represented by commits, not duplicated files.

## Future Organization

This repository may eventually include additional categories such as:

```text
prompts/
├── agents/
├── architecture/
├── bug-fixing/
├── code-review/
├── documentation/
├── refactoring/
├── testing/
└── workflows/
```

New categories should be introduced only when real reusable prompts justify them.

The repository structure should evolve from actual usage rather than anticipated complexity.

## Summary

The core organization strategy is:

```text
Reusable knowledge
        ↓
dev-prompts repository
        ↓
Git versioning
        ↓
selected symbolic links
        ↓
individual projects
```

while:

```text
Project-specific knowledge
        ↓
project repository
        ↓
AGENTS.md / commands / workflows / guidelines
```

The goal is to maintain reusable AI instructions without contaminating individual projects with unrelated context.
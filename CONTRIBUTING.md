# Contributing

This document defines how prompts, guidelines, and reusable AI workflows should be created, changed, reviewed, tested, and maintained in this repository.

Prompts in this repository are treated as software artifacts.

Changes to prompts may alter AI behavior, so they should be intentional, traceable, and reviewable.

## Core Principles

Contributions should favor:

- clear purpose;
- explicit scope;
- minimal necessary context;
- reuse across projects;
- evidence-based instructions;
- predictable output when appropriate;
- clear separation between generic and project-specific knowledge;
- incremental evolution;
- traceable behavioral changes.

Avoid adding complexity without a demonstrated need.

## What Belongs in This Repository

This repository is intended for reusable prompts, guidelines, and workflows that can reasonably be applied across multiple software projects.

Good candidates include:

- code-review prompts;
- bug-investigation workflows;
- test-generation prompts;
- architecture-analysis prompts;
- documentation prompts;
- reusable development utilities;
- reusable language or framework guidelines;
- reusable agent workflows.

Project-specific instructions should normally remain in the project that owns them.

Examples include:

- project-specific `AGENTS.md`;
- internal business rules;
- repository-specific architecture constraints;
- client-specific instructions;
- project-specific workflows;
- confidential development guidelines.

A useful question is:

> Would this artifact still make sense, mostly unchanged, in another project?

If the answer is yes, it may belong here.

If the answer is no, it probably belongs in the project repository.

## Repository Organization

Prompts should be categorized according to their primary purpose.

Categories should be introduced from actual usage rather than anticipated future needs.

Do not create large empty directory structures simply because they may be useful later.

A prompt folder should generally follow this structure:

```text
prompt-name/
├── README.md
└── prompt.md
```

Where:

```text
README.md
→ human-facing documentation

prompt.md
→ canonical prompt consumed by humans or AI tools
```

Additional files may be introduced when there is a clear requirement.

## Prompt Documentation

Every reusable prompt should have human-readable documentation.

The prompt `README.md` should normally describe:

- prompt name;
- objective;
- link to the canonical prompt;
- when to use it;
- when not to use it;
- expected inputs;
- expected outputs;
- known limitations;
- project-context expectations;
- tested models, when available;
- evaluation status;
- relevant observations;
- recent changelog.

The documentation should explain how to use the prompt without requiring someone to reverse-engineer `prompt.md`.

## Canonical Prompt

Each reusable prompt should have one canonical source file.

Prefer:

```text
prompt.md
```

Avoid manually maintained variants such as:

```text
prompt-final.md
prompt-new.md
prompt-v2.md
prompt-final-final.md
prompt-best.md
prompt-last.md
```

Use Git history to represent evolution.

If multiple variants are genuinely required, their purpose must be explicit rather than encoded through informal filenames.

## Prompt Design

Reusable prompts should favor the following concepts when appropriate:

- Persona and Scope;
- Objective;
- Inputs;
- Output Format;
- Quality Criteria;
- Assumptions;
- Negative Instructions;
- Error Handling;
- Workflow.

These are design tools, not mandatory sections.

Do not include a section merely because a template contains it.

Every instruction should serve a clear operational purpose.

## Avoid Prompt Bloat

More instructions do not automatically produce better results.

Excessive prompt content may:

- consume unnecessary tokens;
- increase ambiguity;
- introduce contradictory instructions;
- increase latency;
- reduce portability across models;
- make maintenance harder.

Prefer the smallest prompt that reliably provides the required behavior.

Do not remove context that is necessary for correctness merely to reduce token count.

## Generic and Specialized Prompts

Prefer separating generic tasks from reusable technical specialization.

For example:

```text
generic automated-testing prompt
        +
Go testing guidelines
        =
Go-specific test-generation behavior
```

Instead of duplicating the entire prompt for every technology.

Possible specialization dimensions include:

```text
languages/
frameworks/
infrastructure/
testing/
security/
```

Specializations should only be created when there is real reusable knowledge to store.

## Project Context

Generic prompts should not silently encode project-specific assumptions.

When project-specific instructions exist, the reusable prompt should be composed with artifacts such as:

```text
AGENTS.md
CLAUDE.md
architecture documentation
repository guidelines
testing conventions
```

Conceptually:

```text
reusable prompt
      +
technical specialization
      +
project instructions
      +
task input
      =
contextualized execution
```

## Version Control

All meaningful changes should be versioned with Git.

Versioning provides:

- history;
- diffs;
- authorship;
- rollback;
- branches;
- pull requests;
- review;
- behavioral traceability.

A prompt should be treated as changed whenever its expected behavior changes.

Examples include:

- changing scope;
- adding or removing constraints;
- modifying negative instructions;
- changing output format;
- adding examples;
- changing workflow steps;
- changing evaluation criteria;
- resolving ambiguity;
- changing failure behavior.

## Commit Messages

Commit messages should communicate the behavioral intent of the change whenever possible.

Examples:

```text
feat: add reusable code review prompt
```

```text
feat: add bug investigation workflow
```

```text
fix: prevent code review prompt from suggesting unrelated refactors
```

```text
fix: require evidence for security findings
```

```text
refactor: simplify architecture analysis prompt
```

```text
docs: document code review prompt usage
```

```text
docs: add prompt contribution guidelines
```

Avoid commit messages that provide no useful context, such as:

```text
update prompt
changes
fix stuff
new version
```

## Personal Workflow

For prompts maintained by a single developer, formal pull requests are optional.

A lightweight workflow is sufficient:

```text
identify need
      ↓
edit prompt
      ↓
test behavior
      ↓
review diff
      ↓
commit
      ↓
reuse
```

Git versioning is still recommended even for personal prompts.

## Team Workflow

For prompts shared by a team, use a collaborative workflow similar to source code.

Recommended flow:

```text
identify behavioral problem
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

A pull request should ideally explain:

- what problem was observed;
- what behavior exists today;
- what changed;
- what behavior is expected after the change;
- how the new version was tested;
- any relevant trade-offs.

## Reviewing Prompt Changes

Prompt review should focus on behavior rather than prose style alone.

Reviewers should ask:

- Is the objective clear?
- Is the scope clear?
- Could instructions conflict?
- Was unnecessary context added?
- Was necessary context removed?
- Could the change introduce unintended behavior?
- Is the output contract still correct?
- Are assumptions explicit where needed?
- Are negative instructions justified?
- Does the prompt remain reusable?
- Has project-specific knowledge leaked into a generic prompt?
- Was the change tested?

Readable wording is important, but semantic behavior is the primary concern.

## Testing Prompt Changes

Prompts should be tested against representative tasks before significant behavioral changes are accepted.

At minimum, manually compare:

```text
previous prompt
      vs.
candidate prompt
```

using equivalent inputs.

Observe differences in:

- correctness;
- instruction adherence;
- consistency;
- verbosity;
- hallucination or speculation;
- output format;
- scope adherence;
- useful findings;
- false positives;
- latency when relevant;
- token usage when relevant.

Formal evaluation may be introduced for prompts where objective metrics are available.

## Prompt Evaluation

Prompt evaluation can range from manual review to automated benchmark datasets.

Possible metrics include:

- task success rate;
- useful finding precision;
- false-positive rate;
- hallucination rate;
- format compliance;
- instruction adherence;
- severity classification accuracy;
- regression detection;
- token consumption;
- latency.

Not every productivity prompt can be evaluated with a single deterministic score.

When evaluation is subjective, document the evaluation method and examples used.

## Model Considerations

The same prompt may behave differently across:

- model families;
- model versions;
- inference settings;
- tool environments;
- agent runtimes.

When relevant, document models used during testing.

Suggested format:

```text
Model:
<model name/version>

Date:
<YYYY-MM-DD>

Scenario:
<what was tested>

Result:
<observation>

Notes:
<relevant differences or limitations>
```

Do not silently optimize a generic prompt around behavior unique to one model without documenting that dependency.

## Prompt Evolution

Prompts should evolve from real usage.

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
review
      ↓
new version
```

Example:

```text
Problem:
The coding agent performs unrelated refactors while fixing bugs.

Diagnosis:
The prompt does not explicitly restrict opportunistic changes.

Change:
Add a minimal-change policy and negative instruction.

Expected behavior:
Bug fixes remain limited to the reported problem.
```

Repeated failures may eventually become reusable guidelines.

## Changelog

Prompt-level documentation may contain a small changelog describing recent important behavioral changes.

Example:

```markdown
## Changelog

### 2026-10-06

- Added evidence requirements.
- Reduced speculative findings.

### 2026-10-05

- Initial version.
```

This changelog does not replace Git history.

Its purpose is to give users a quick human-readable explanation of recent behavioral evolution.

## Security and Public Repository Rules

This repository is public.

Never commit:

- API keys;
- credentials;
- tokens;
- private URLs;
- internal customer data;
- confidential business rules;
- proprietary source code;
- sensitive infrastructure details;
- private prompts owned by clients or employers.

Before committing a new artifact, verify that it is safe for public distribution.

Project-specific or confidential instructions belong in the appropriate private repository.

## Symbolic Links and Project Consumption

Projects should expose only the reusable prompts they actually need.

A recommended local approach is:

```text
project/
└── .prompts/
    ├── code-review.md
    └── ...
```

where the files are symbolic links to this repository.

Local reusable prompt links should normally be excluded from the target project's Git repository:

```gitignore
.prompts/
```

Project-owned prompts and agent instructions should remain versioned in the project itself.

## Definition of Done

A new reusable prompt is ready to merge when:

- its purpose is clear;
- its scope is explicit;
- the canonical `prompt.md` exists;
- its `README.md` exists;
- its intended use is documented;
- obvious project-specific assumptions have been removed;
- it has been tested at least manually;
- known limitations are documented when relevant;
- no sensitive information is included;
- Git diff has been reviewed.

A modification to an existing prompt is ready when:

- the behavioral reason for the change is understood;
- the change has been tested;
- the documentation remains accurate;
- relevant changelog information has been updated;
- no unrelated changes were introduced.

## Final Principle

Treat prompts as evolving software assets.

A useful prompt should be:

```text
discoverable
versioned
documented
testable
reviewable
reusable
maintainable
```

The objective is not to create the largest prompt library.

The objective is to maintain a small, reliable collection of AI instructions that demonstrably improve software-development workflows.
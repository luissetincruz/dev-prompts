# Code Review

Reusable prompt for performing focused, evidence-based code reviews.

The prompt is designed to identify concrete engineering risks in code changes while avoiding speculative findings, stylistic preferences, and unrelated refactoring suggestions.

## Prompt

[View the raw prompt](./prompt.md)

## Objective

The purpose of this prompt is to review code changes and identify meaningful problems related to:

- correctness;
- regressions;
- security;
- reliability;
- error handling;
- edge cases;
- concurrency and state;
- performance;
- maintainability;
- test coverage;
- explicit project rules.

The goal is not to maximize the number of review comments.

The goal is to identify the smallest set of findings that materially improves the correctness, safety, reliability, and maintainability of the reviewed change.

## When to Use

Use this prompt when reviewing:

- Git diffs;
- pull requests;
- commits;
- changed files;
- focused source-code changes;
- pre-commit changes;
- implementation changes before merge.

Typical examples:

```text
Review the current uncommitted changes.
```

```text
Review this pull request.
```

```text
Review the changes introduced by this commit.
```

```text
Review these changed files for bugs, regressions, security issues, and missing tests.
```

## When Not to Use

This prompt is not intended to perform:

- a complete codebase audit;
- architecture redesign;
- broad refactoring;
- dependency auditing;
- full security assessment;
- performance benchmarking;
- implementation of fixes.

Use a more specialized prompt when the objective is broader than reviewing a focused set of changes.

## Expected Inputs

The prompt can work with one or more of the following:

- Git diff;
- pull request changes;
- commit changes;
- source files;
- related tests;
- configuration files;
- dependency files;
- issue or task descriptions;
- project documentation;
- project-specific instructions.

The quality of the review depends on the quality of the context provided.

## Project Context

This is a generic reusable prompt.

It does not contain assumptions about a specific:

- company;
- repository;
- framework;
- programming language;
- architecture;
- domain;
- business rule.

When project-specific instructions are available, combine this prompt with them.

Examples:

```text
AGENTS.md
```

```text
CLAUDE.md
```

```text
repository guidelines
```

```text
architecture documentation
```

```text
testing conventions
```

Conceptually:

```text
generic code-review prompt
        +
project-specific instructions
        +
current code changes
        =
contextualized code review
```

## Example Usage

A coding agent can be instructed with something like:

```text
Perform a code review of the current uncommitted changes.

Follow the reusable review instructions in:

.prompts/code-review.md

Also follow all project-specific instructions available in the repository.

Review only the current changes and the surrounding code required to validate them.

Do not modify any files.
```

The exact invocation depends on the AI tool being used.

## Review Philosophy

The prompt follows a few core principles.

### Evidence Over Speculation

Every finding should be supported by the available code or context.

The model should not fabricate:

- runtime behavior;
- logs;
- benchmarks;
- vulnerabilities;
- requirements;
- business rules;
- production incidents.

If something cannot be confirmed, it should be marked as uncertain.

### Defects Over Style

The review should prioritize:

- bugs;
- regressions;
- security risks;
- reliability issues;
- meaningful performance problems;
- important maintainability risks;
- missing relevant tests.

Purely stylistic preferences should not become review findings.

### Focused Scope

The review should focus primarily on the changed code.

Surrounding code may be inspected when necessary to understand:

- contracts;
- dependencies;
- side effects;
- existing behavior;
- possible regressions.

The prompt should not turn a focused review into a general audit of the entire repository.

### Minimal Useful Findings

The objective is not to generate many comments.

A review with two strong, evidence-based findings is better than a review with fifteen speculative observations.

## Severity Levels

The prompt classifies findings using four severity levels.

### Critical

Issues that may cause:

- severe security vulnerabilities;
- data loss or corruption;
- major production outages;
- catastrophic failures;
- violation of critical system guarantees.

### High

Issues that may cause:

- incorrect application behavior;
- important regressions;
- serious reliability problems;
- meaningful security risks;
- failure of core use cases.

### Medium

Concrete issues that should be corrected but are unlikely to cause immediate severe failure.

Examples:

- relevant edge cases;
- weak error handling;
- maintainability problems with clear impact;
- missing important tests.

### Low

Minor but concrete engineering issues with limited impact.

`Low` should never be used for personal style preferences.

## Output Structure

The prompt produces a structured review containing:

```text
# Code Review

Critical: <count>
High: <count>
Medium: <count>
Low: <count>
```

Each finding includes:

```text
Severity
File
Location
Problem
Impact
Evidence
Recommended correction
```

Findings are ordered from highest to lowest severity.

If no meaningful problems are found, the expected result is:

```text
# Code Review

No significant issues found.
```

## Missing Context

When missing information prevents a reliable conclusion, the review may include:

```text
## Missing Context
```

Only information that materially affects the review should be requested.

Examples:

- missing API contract;
- missing schema;
- unavailable project requirement;
- missing related implementation;
- unavailable test behavior.

Missing context should not be used as justification for speculation.

## Tested Models

Not formally evaluated yet.

When this prompt is tested systematically, record the models and relevant observations here.

Suggested format:

```text
Model:
<model name>

Date:
<YYYY-MM-DD>

Result:
<short observation>

Notes:
<any relevant behavioral differences>
```

## Evaluation Status

Formal prompt evaluation has not yet been implemented.

Future evaluation should consider metrics such as:

- useful finding precision;
- false-positive rate;
- speculative finding rate;
- severity classification quality;
- adherence to project instructions;
- duplicate finding rate;
- ability to detect regressions;
- review conciseness.

## Known Limitations

The review can only reason from the context available to the model.

It may not reliably identify issues that depend on:

- unavailable runtime state;
- production data;
- hidden infrastructure;
- external service behavior;
- undocumented business requirements;
- unavailable files;
- behavior outside the provided context.

A code review generated by an LLM should be treated as an additional engineering review mechanism, not as a replacement for:

- automated tests;
- static analysis;
- security tooling;
- human review;
- runtime validation.

## Maintenance

When changing `prompt.md`, consider updating this document if the change affects:

- purpose;
- supported use cases;
- output format;
- severity rules;
- review criteria;
- known limitations;
- recommended usage.

Git remains the source of truth for the complete history.

This README should provide a concise human-readable view of the prompt's current behavior.

## Changelog

### 2026-10-05

Initial version.

- Added a generic professional code-review persona.
- Added focused review scope.
- Added review criteria for correctness, regressions, security, error handling, edge cases, concurrency, performance, maintainability, tests, and project rules.
- Added severity classification.
- Added evidence requirements.
- Added safeguards against speculative findings.
- Added structured output format.
- Added missing-context handling.
- Added quality criteria.
- Added an explicit review workflow.
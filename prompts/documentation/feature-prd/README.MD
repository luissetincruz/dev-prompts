# Feature PRD

Reusable interview-driven prompt for creating clear, structured, and actionable Feature Product Requirements Documents (Feature PRDs).

The prompt guides the user through requirements elicitation, identifies missing or contradictory information, distinguishes confirmed requirements from hypotheses, and produces a maintainable PRD for use by humans and AI-assisted development workflows.

## Prompt

[View the raw prompt](./prompt.md)

## Objective

The purpose of this prompt is to help define software features before detailed technical design or implementation begins.

It is designed to:

- clarify what is being built and why;
- capture the current context and problem;
- identify relevant users and stakeholders;
- define goals and measurable success criteria;
- establish explicit scope boundaries;
- collect functional and non-functional requirements;
- document important user, system, or integration flows;
- identify dependencies;
- preserve known technical constraints and existing decisions;
- surface risks and unresolved questions;
- define verifiable acceptance criteria;
- describe how the feature should be validated;
- make assumptions and uncertainty explicit;
- generate a structured Feature PRD in Markdown;
- optionally provide the same information as structured JSON.

The goal is not to create the largest possible document.

The goal is to produce the smallest document that reliably communicates the feature's intent, requirements, constraints, and success conditions.

## When to Use

Use this prompt when a software feature has enough product or operational context to justify a dedicated requirements document.

Typical cases include features with:

- their own objectives;
- measurable outcomes;
- meaningful business rules;
- relevant scope decisions;
- multiple functional requirements;
- non-functional requirements;
- important user or system flows;
- dependencies across systems or teams;
- material risks;
- acceptance criteria;
- unresolved product questions;
- known technical constraints that affect the requirements.

Examples include:

```text
Define the PRD for a centralized rate-limiting capability used by multiple APIs.
```

```text
Create a Feature PRD for enterprise authentication with SSO, MFA, and tenant-specific access policies.
```

```text
Help me define a PRD for a shared product catalog consumed by storefront, checkout, and internal operations.
```

The prompt is also useful when requirements exist informally across:

- tickets;
- chats;
- product notes;
- repository documentation;
- architecture documents;
- stakeholder discussions;
- existing code;
- previous specifications.

In those cases, the prompt should reuse existing context and ask only for information that is materially missing.

## When Not to Use

This prompt is usually unnecessary for:

- trivial text changes;
- small UI adjustments;
- simple bug fixes;
- routine dependency updates;
- implementation tasks whose requirements are already complete;
- isolated refactors with no product-level decision;
- purely technical migrations with no meaningful product requirement;
- detailed architecture design;
- architectural decision records;
- operational runbooks;
- task breakdowns;
- direct code implementation.

Examples that may not justify a dedicated Feature PRD:

```text
Change the label of a button from "Send" to "Continue".
```

```text
Upgrade a library from one patch version to another.
```

```text
Rename an internal variable.
```

If the requested change appears too small to justify a Feature PRD, the prompt should explain this briefly and allow the user to decide whether to continue.

For detailed technical design, use a dedicated Design Doc.

For architectural decision rationale, use an ADR.

For operational recovery procedures, use a Runbook.

## Expected Inputs

The prompt can work with one or more of the following:

- a feature idea;
- a problem statement;
- product documentation;
- project documentation;
- existing requirements;
- issue or ticket descriptions;
- user stories;
- business rules;
- architecture documentation;
- ADRs;
- repository guidelines;
- technical constraints;
- screenshots;
- existing code;
- API contracts;
- stakeholder notes;
- research;
- metrics;
- acceptance criteria.

A complete specification is not required before using the prompt.

The interview is intended to discover missing information incrementally.

The quality of the resulting PRD depends on the quality and authority of the context available.

## Project Context

This is a generic reusable prompt.

It does not contain assumptions about a specific:

- company;
- repository;
- programming language;
- framework;
- database;
- cloud provider;
- architecture;
- business domain;
- delivery process.

Project-specific knowledge should remain in the project that owns it.

When project context is available, combine this prompt with artifacts such as:

```text
AGENTS.md
```

```text
CLAUDE.md
```

```text
product documentation
```

```text
architecture documentation
```

```text
ADRs
```

```text
repository guidelines
```

```text
existing feature specifications
```

Conceptually:

```text
generic feature-PRD prompt
        +
project-specific instructions
        +
existing project documentation
        +
feature context
        =
contextualized Feature PRD
```

The prompt should use existing context before asking the user to repeat information.

## Interview Workflow

The prompt follows an incremental requirements-elicitation workflow.

The main sequence is:

```text
analyze existing context
        ↓
feature summary
        ↓
context and problem
        ↓
users and stakeholders
        ↓
goals and success metrics
        ↓
scope
        ↓
functional requirements
        ↓
non-functional requirements
        ↓
user or system flows
        ↓
dependencies
        ↓
known technical constraints
        ↓
risks and mitigations
        ↓
acceptance criteria
        ↓
testing and validation
        ↓
open questions and hypotheses
        ↓
consistency check
        ↓
final confirmation
        ↓
Feature PRD
```

The workflow is adaptive.

If information is already available and sufficiently clear, the prompt should not ask for it again.

The prompt asks one primary question at a time so the user can refine the feature incrementally without answering a large questionnaire in one message.

## Requirements Elicitation Principles

### Existing Context First

The prompt should inspect available information before asking questions.

If a requirement, constraint, or decision is already clearly supported by authoritative context, it should be reused rather than asked again.

### No Silent Invention

The prompt must not fabricate:

- business rules;
- success metrics;
- deadlines;
- compliance obligations;
- integrations;
- architecture;
- performance targets;
- availability targets;
- security requirements;
- implementation technologies.

Missing information should result in:

- a question;
- an explicit unknown;
- or an AI suggestion clearly marked as a hypothesis.

### One Primary Question at a Time

The interview should remain incremental and easy to answer.

A question may include:

- a short explanation;
- examples;
- suggested options;
- a small list of choices.

It should not combine unrelated questions into one turn.

### Preserve Corrections

When the user changes or corrects a previously collected requirement, the prompt should:

- replace the obsolete information;
- use the corrected value going forward;
- reconsider dependent requirements when necessary.

## Confirmed Information, Hypotheses, and Unknowns

The prompt distinguishes between:

```text
confirmed
hypothesis
unknown
```

Information may come from sources such as:

```text
user
provided_context
ai_suggestion
```

`confirmed` means the information is explicitly supported by the user or authoritative project context.

`hypothesis` means the information may be reasonable but has not yet been confirmed.

`unknown` means the information is still missing.

An AI-generated suggestion must never silently become a confirmed requirement.

For example:

```text
Target:
p95 additional latency <= 10 ms

Status:
hypothesis

Source:
ai_suggestion
```

remains a provisional suggestion until the user confirms, changes, or rejects it.

This distinction is especially important when the PRD will later be consumed by other AI agents.

## Product Requirements and Technical Design

The prompt is intentionally focused on feature-level product and system requirements.

It may record known technical information when that information is already required or approved, such as:

- mandated protocols;
- required deployment environments;
- approved technologies;
- compatibility requirements;
- existing architectural decisions;
- security or regulatory constraints.

It should not independently invent technical design.

For example:

```text
Requirement:
The rate limiter must work consistently across multiple application instances.
```

belongs naturally in the PRD.

A decision such as:

```text
Implementation:
Use Redis with a sliding-window algorithm.
```

normally belongs in a Technical Design Doc unless it is already an approved project constraint.

Conceptually:

```text
Feature PRD
→ what, why, behavior, scope, constraints, success

Technical Design Doc
→ how the feature will be implemented
```

A Feature PRD may provide input to a later Design Doc, but it should not silently replace one when detailed design is necessary.

## Stable IDs and Traceability

The prompt uses stable identifiers where useful.

Examples include:

```text
GOAL-001
FR-001
NFR-001
FLOW-001
DEP-001
DEC-001
RISK-001
AC-001
VAL-001
HYP-001
```

These IDs make it easier to relate the PRD to later artifacts.

Conceptually:

```text
FR-001
   ↓
AC-001
   ↓
Design
   ↓
Task
   ↓
Code
   ↓
Test
```

The prompt does not require every sentence to have an identifier.

IDs should be used when they improve traceability and downstream consumption.

## Functional Requirements

Functional requirements describe observable capabilities and behavior.

Each requirement may contain:

```text
ID
Name
Description
Priority
Main Flow
Alternative Flows
Known Errors or Failure Conditions
Related Acceptance Criteria
```

The prompt should prefer behavior over implementation details.

For example:

```text
FR-001 — Enforce request limits per client

The system must evaluate each incoming request against the configured limit for the identified client.
```

is preferable to embedding an unconfirmed storage or framework decision in the requirement.

## Non-Functional Requirements

Non-functional requirements describe quality attributes and operational constraints.

Common categories include:

- performance;
- latency;
- availability;
- reliability;
- scalability;
- security;
- privacy;
- accessibility;
- observability;
- compatibility;
- compliance;
- recovery;
- data retention.

When practical, requirements should be measurable.

Prefer:

```text
p95 additional latency <= 10 ms
```

over:

```text
The operation should be fast.
```

Numeric targets must not be invented.

When the user does not yet know a value, the prompt may suggest a provisional starting point, but it must remain explicitly marked as a hypothesis until confirmed.

## User and System Flows

The prompt can capture:

```text
user flows
system flows
integration flows
```

A user flow should not be forced onto a backend-only or infrastructure feature.

For example, a platform capability may be better represented as:

```text
1. Client sends request.
2. Gateway identifies the client.
3. Policy is evaluated.
4. The request is accepted or rejected.
5. The client receives the appropriate response.
```

The purpose of the flow is to clarify observable behavior and sequence, not to prematurely define internal implementation.

## Acceptance Criteria

Acceptance criteria define observable conditions that indicate whether the feature satisfies its requirements.

They should be:

- clear;
- verifiable;
- testable when practical;
- traceable to relevant requirements.

Prefer:

```text
When a client exceeds its configured request limit,
subsequent requests are rejected according to the defined policy.
```

over:

```text
The rate limiter works correctly.
```

Acceptance criteria are particularly useful for later:

- implementation validation;
- test generation;
- code review;
- AI-assisted development workflows.

## Testing and Validation

The PRD may describe how requirements should be validated.

Examples include:

- unit or automated tests;
- integration tests;
- end-to-end tests;
- load tests;
- security validation;
- accessibility validation;
- observability checks;
- manual acceptance;
- rollout validation.

The PRD should describe what requires validation without unnecessarily prescribing test implementation details.

## Consistency Checks

Before generating the final PRD, the prompt performs a consistency review.

It checks questions such as:

- Does the feature summary match the problem?
- Are goals connected to the problem?
- Are metrics or unresolved metrics explicit?
- Were any numeric targets invented?
- Does `In Scope` contradict `Out of Scope`?
- Are functional requirements uniquely identified?
- Are non-functional requirements measurable when practical?
- Are flows consistent with the requirements?
- Are dependencies explicit?
- Are technical constraints actually confirmed?
- Are risks meaningful?
- Are acceptance criteria observable?
- Are hypotheses still marked as hypotheses?
- Are important unknowns visible?
- Were unsupported implementation decisions introduced?

When a material problem prevents a reliable PRD, the prompt should request clarification instead of producing a misleading final document.

## Expected Output

The primary output is a Feature PRD in Markdown.

Depending on the available information, the document may contain:

```text
Document Information
Summary
Context and Problem
Users and Stakeholders
Goals and Success Metrics
Scope
Functional Requirements
Non-Functional Requirements
User and System Flows
Dependencies
Known Technical Constraints and Existing Decisions
Risks and Mitigations
Acceptance Criteria
Testing and Validation
Open Questions
Hypotheses
References
```

Sections that do not add value should be omitted.

The prompt should not create empty sections simply because the template supports them.

## Optional JSON Output

After generating the Markdown PRD, the prompt can optionally generate a structured JSON representation.

The JSON is intended for:

- programmatic consumption;
- automation;
- agent workflows;
- requirement filtering;
- downstream tooling;
- structured context exchange.

The Markdown and JSON outputs must represent the same requirements.

They should not become two independent interpretations of the feature.

Conceptually:

```text
requirements state
        ├── Markdown → human-readable representation
        └── JSON     → structured representation
```

If both artifacts are stored in a project, teams should avoid maintaining them independently as separate sources of truth.

## Example Usage

A user may start with very little context:

```text
I need to define a Feature PRD for centralized rate limiting across our APIs.
```

The prompt should begin the interview and ask only the next meaningful missing question.

A richer invocation might be:

```text
Create a Feature PRD for the authentication capability described in the attached product notes.

Use the existing architecture documentation and ADRs as context.

Do not invent requirements that are not documented.

Ask me only for information that is materially missing.
```

Another example:

```text
Review the existing issue, repository documentation, and requirements notes.

Use them as context to build a Feature PRD.

Identify contradictions or missing decisions before generating the final document.
```

The exact invocation depends on the AI tool and available context.

## Known Limitations

The quality of the PRD depends on the information available to the model.

The prompt cannot independently verify:

- business priorities;
- stakeholder agreement;
- production behavior;
- undocumented requirements;
- hidden regulatory obligations;
- external contracts;
- infrastructure not present in the context;
- correctness of project documentation;
- whether an existing architectural decision is still valid.

A polished PRD is not proof that the underlying assumptions are correct.

AI-assisted requirements elicitation should not replace appropriate validation with:

- product stakeholders;
- domain experts;
- engineering;
- security;
- compliance;
- operations;
- end users, when relevant.

The prompt may identify uncertainty, but it cannot resolve unknown business decisions without authoritative input.

## Tested Models

Not formally evaluated yet.

When this prompt is tested systematically, record the models and relevant observations here.

Suggested format:

```text
Model:
<model name>

Date:
<YYYY-MM-DD>

Scenario:
<what was tested>

Result:
<short observation>

Notes:
<any relevant behavioral differences>
```

## Evaluation Status

Formal prompt evaluation has not yet been implemented.

Initial evaluation should consider scenarios such as:

- a trivial change that may not justify a PRD;
- a feature with complete context;
- a feature with missing metrics;
- contradictory scope information;
- conflicting project documents;
- unknown non-functional targets;
- an AI-suggested hypothesis that must remain unconfirmed;
- an existing technical decision that must be preserved;
- a feature that requires a separate Technical Design Doc.

Useful evaluation criteria may include:

- instruction adherence;
- one-primary-question-per-turn compliance;
- requirement invention rate;
- hypothesis-labeling accuracy;
- missing-context detection;
- contradiction detection;
- scope consistency;
- requirement traceability;
- measurable NFR quality;
- acceptance-criteria quality;
- separation between requirements and technical design;
- Markdown format compliance;
- JSON validity;
- semantic consistency between Markdown and JSON;
- interview efficiency;
- unnecessary-question rate;
- overall PRD usefulness.

Pairwise evaluation may also be useful when comparing future versions of this prompt.

## Maintenance

When changing `prompt.md`, consider updating this document if the change affects:

- interview workflow;
- scope;
- requirements structure;
- status or source rules;
- output format;
- stable IDs;
- technical-design boundaries;
- consistency checks;
- optional JSON behavior;
- known limitations;
- recommended usage.

Git remains the source of truth for the complete history.

This README should provide a concise human-readable view of the prompt's current behavior.

## Changelog

### 2026-10-16

Initial version.

- Added an interview-driven Feature PRD workflow.
- Added reuse of existing project context before asking questions.
- Added one-primary-question-per-turn behavior.
- Added explicit handling of confirmed information, hypotheses, and unknowns.
- Added source tracking for user input, provided context, and AI suggestions.
- Added stable IDs for requirements and related artifacts.
- Added functional and non-functional requirement structures.
- Added user, system, and integration flow support.
- Added dependency and risk tracking.
- Added acceptance criteria and validation planning.
- Added consistency checks before final document generation.
- Added safeguards against invented requirements and technical decisions.
- Added separation between Feature PRD and detailed Technical Design.
- Added Markdown output with optional structured JSON representation.

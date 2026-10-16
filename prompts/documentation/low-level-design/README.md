# Low-Level Design

Reusable context-aware prompt for creating implementation-ready, traceable, and maintainable Low-Level Design (LLD) documents.

The prompt helps the user translate confirmed product requirements, architecture, feature behavior, existing code, tests, and project conventions into concrete implementation structure without silently inventing design decisions.

It is intentionally lower-level than the High-Level Design and Feature Design prompts, while remaining separate from production code and implementation task planning.

## Prompt

[View the raw prompt](./prompt.md)

## Objective

The purpose of this prompt is to transform upstream requirements and technical design into an implementation-level design that removes ambiguity before coding begins.

It is designed to:

- reuse Product PRDs, Feature PRDs, HLDs, FDDs, ADRs, RFCs, research, codebase context, tests, schemas, and project conventions before asking questions;
- identify implementation-level design gaps;
- define module and package boundaries;
- define classes, services, internal interfaces, and responsibilities;
- define important data structures and internal schemas;
- define non-trivial algorithms and decision logic;
- define detailed internal call sequences;
- define state and state transitions when relevant;
- define persistence and transaction boundaries;
- define concurrency and synchronization behavior when relevant;
- define validation and internal error handling;
- define implementation-level observability hooks;
- capture security and sensitive-data concerns;
- define testability and verification strategy;
- identify implementation risks and trade-offs;
- preserve open questions, pending decisions, hypotheses, and references;
- generate a structured LLD in Markdown;
- optionally provide the same information as structured JSON.

The goal is not to generate production code.

The goal is to produce the smallest LLD that reliably removes implementation ambiguity while preserving upstream product and architectural intent.

## Position in the Documentation Flow

The LLD sits below product, architecture, and feature-level design artifacts.

Conceptually:

```text
Product PRD
        ↓
Feature PRD
        ↓
High-Level Design
        ↓
Feature Design Doc
        ↓
Low-Level Design
        ↓
Implementation Plan
        ↓
Code
```

Each artifact has a different responsibility:

```text
Product PRD
→ product-level why, outcomes, scope, capabilities, KPIs

Feature PRD
→ feature-level requirements and acceptance criteria

High-Level Design
→ system-level architecture

Feature Design Doc
→ detailed feature behavior and public contracts

Low-Level Design
→ internal implementation structure and mechanics

Implementation Plan
→ execution sequence and tasks

Code
→ final implementation
```

The LLD should refine upstream artifacts rather than silently replace them.

## LLD vs. Feature Design Doc

The Feature Design Doc defines feature behavior that consumers and surrounding systems depend on.

The Low-Level Design defines how that behavior will be implemented internally.

For example:

```text
FDD
→ POST /payments is idempotent
→ duplicate requests return the existing result
→ payment state changes are observable
→ timeout behavior is defined
```

while the LLD may define:

```text
LLD
→ PaymentService owns orchestration
→ IdempotencyRepository stores operation keys
→ PaymentAttempt is the persistence model
→ transaction TX-001 protects duplicate creation
→ ALG-001 resolves existing vs. new requests
```

The LLD must preserve the behavior defined by the FDD.

It should not silently modify public contracts, compatibility guarantees, or externally observable errors.

## LLD vs. Implementation Plan

An LLD explains **what the implementation structure should be**.

An implementation plan explains **how the team or agent should execute the work**.

For example:

```text
LLD
→ introduce PaymentIdempotencyService
→ define IdempotencyStore interface
→ use transaction TX-001 around lookup + insert
```

An implementation plan may later say:

```text
1. create the IdempotencyStore interface;
2. implement the PostgreSQL adapter;
3. add PaymentIdempotencyService;
4. update PaymentService;
5. add integration tests;
6. deploy behind a feature flag.
```

The LLD should not become a task list.

## When to Use

Use this prompt when implementation contains enough internal complexity that coding directly from an FDD or ticket would require meaningful assumptions.

Typical cases include:

- a new backend module;
- a new domain service;
- a complex application service;
- a significant internal refactor;
- a feature with multiple collaborating classes or modules;
- non-trivial persistence behavior;
- transaction boundaries;
- concurrency or synchronization;
- complex validation;
- non-trivial algorithms;
- state machines;
- multiple data representations;
- internal adapter or repository design;
- new internal interfaces;
- migration-sensitive code;
- features where testability needs explicit design;
- high-risk implementation changes;
- implementation involving significant trade-offs.

Examples include:

```text
Create an LLD for implementing idempotent payment processing inside the existing checkout service.
```

```text
Help me design the internal modules, repositories, transactions, and state transitions for the rate-limiting feature defined in the FDD.
```

```text
Create an LLD for refactoring the notification pipeline without changing its public event contracts.
```

The prompt is also useful when implementation context already exists across:

- FDDs;
- HLDs;
- Feature PRDs;
- Product PRDs;
- ADRs;
- RFCs;
- code;
- tests;
- schemas;
- migrations;
- repository documentation;
- coding standards;
- architecture guidelines.

In those cases, the prompt should extract what is already known, identify contradictions, and ask only about material implementation gaps.

## When Not to Use

This prompt is usually unnecessary for:

- trivial changes;
- small bug fixes;
- simple configuration edits;
- routine dependency upgrades;
- isolated one-line changes;
- straightforward CRUD operations already covered by existing patterns;
- code generation from an already complete LLD;
- feature-level requirements definition;
- system-level architecture;
- public contract design;
- implementation task sequencing;
- operational runbooks.

Examples that may not justify a dedicated LLD:

```text
Rename one private method.
```

```text
Add one validation using an existing project pattern.
```

```text
Update a package patch version.
```

If the requested change appears too small for an LLD, the prompt should explain this briefly and allow the user to decide whether to continue.

For product requirements, use a Product PRD.

For feature requirements, use a Feature PRD.

For system architecture, use a High-Level Design.

For detailed feature behavior and public contracts, use a Feature Design Doc.

For delivery sequencing, use an implementation plan.

## Expected Inputs

The prompt can work with one or more of the following:

- a Product PRD;
- a Feature PRD;
- a High-Level Design;
- a Feature Design Doc;
- ADRs;
- RFCs;
- technical research;
- Deep Research reports;
- source code;
- repository structure;
- package structure;
- existing classes;
- interfaces;
- schemas;
- APIs;
- event contracts;
- queue contracts;
- database schemas;
- migrations;
- tests;
- coding standards;
- repository guidelines;
- engineering conventions;
- performance requirements;
- security requirements;
- observability requirements;
- platform constraints;
- issue or ticket descriptions.

A complete implementation design does not need to exist before using the prompt.

The prompt is designed to reuse existing context first and then guide the user through the missing implementation-level decisions.

## Project Context

This is a generic reusable prompt.

It does not assume a specific:

- company;
- repository;
- language;
- framework;
- package structure;
- database;
- ORM;
- design pattern;
- dependency-injection style;
- transaction strategy;
- concurrency strategy;
- logging stack;
- test framework;
- cloud provider.

Project-specific implementation conventions should remain in the project that owns them.

When project context is available, combine this prompt with artifacts such as:

```text
Feature Design Doc
```

```text
High-Level Design
```

```text
Feature PRD
```

```text
ADRs / RFCs
```

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
coding standards
```

```text
source code
```

```text
tests
```

Conceptually:

```text
generic LLD prompt
        +
Feature Design Doc
        +
High-Level Design
        +
ADRs / RFCs
        +
repository conventions
        +
codebase and tests
        =
project-aware Low-Level Design
```

The prompt should use existing context before asking the user to repeat information.

## Context-First Workflow

The prompt is intentionally context-first rather than interview-first.

Before asking questions, it should inspect available context and identify:

- upstream requirements;
- confirmed architecture;
- confirmed feature behavior;
- existing code structure;
- existing interfaces;
- schemas;
- tests;
- coding conventions;
- persistence conventions;
- error conventions;
- observability conventions;
- missing implementation decisions;
- contradictions.

Conceptually:

```text
existing context
        ↓
implementation-context extraction
        ↓
gap detection
        ↓
targeted interview
        ↓
consistency check
        ↓
Low-Level Design
```

The interview exists to fill meaningful implementation gaps rather than rediscover information already available.

## Interview Workflow

The main sequence is:

```text
analyze existing context
        ↓
implementation context and boundaries
        ↓
module and component decomposition
        ↓
classes, services, and internal interfaces
        ↓
data structures and internal schemas
        ↓
algorithms and decision logic
        ↓
detailed call sequences
        ↓
state and state transitions
        ↓
persistence and transaction boundaries
        ↓
concurrency and synchronization
        ↓
validation and internal error handling
        ↓
implementation-level observability
        ↓
security and sensitive-data handling
        ↓
testability and verification strategy
        ↓
implementation risks and trade-offs
        ↓
open questions, pending decisions, and hypotheses
        ↓
consistency check
        ↓
final confirmation
        ↓
Low-Level Design
```

The prompt asks one primary question at a time.

It requires confirmation at the end of every interview stage.

Each stage should end with:

- a concise summary;
- remaining ambiguity, hypotheses, open questions, or pending decisions;
- a request for confirmation or correction.

The next stage should not begin until the user confirms or corrects the current one.

## Interview Confirmation Model

Every stage follows this pattern:

```text
question
   ↓
user answer or extracted context
   ↓
3-6 line stage summary
   ↓
hypotheses / unknowns / pending decisions
   ↓
user confirmation
   ↓
next stage
```

If a stage is already fully supported by authoritative context, the prompt should still summarize what it extracted and ask the user to confirm the interpretation.

If the user corrects a previously confirmed stage, the prompt should:

- update the current design state;
- reconsider dependent modules;
- reconsider interfaces;
- reconsider data structures;
- reconsider transactions;
- reconsider concurrency;
- reconsider tests;
- reconsider risks;
- reconfirm affected stages.

## Implementation Design Principles

### Existing Context First

The prompt should inspect available design and code context before asking questions.

If an implementation fact is already clearly supported by authoritative context, it should be reused rather than asked again.

### Preserve Upstream Decisions

The LLD should preserve confirmed behavior and constraints from:

- Product PRDs;
- Feature PRDs;
- HLDs;
- FDDs;
- ADRs;
- RFCs.

If implementation analysis exposes a contradiction, the prompt should surface it explicitly rather than silently working around it.

### No Silent Implementation Decisions

The prompt must not silently choose:

- patterns;
- classes;
- module boundaries;
- algorithms;
- data structures;
- transaction strategies;
- locking strategies;
- retry policies;
- cache policies;
- persistence abstractions;
- method signatures;
- dependency versions;
- numeric limits.

Missing information should result in:

- a question;
- an explicit unknown;
- an open decision;
- a pending decision;
- or an AI suggestion clearly marked as a hypothesis.

### Prefer Existing Project Conventions

If the project already has conventions for:

- package structure;
- dependency injection;
- repositories;
- adapters;
- validation;
- errors;
- logging;
- testing;
- transactions;
- naming;

the prompt should preserve them unless the user explicitly wants to revisit them.

Generic best practice should not silently override local convention.

## Confirmed Information, Hypotheses, and Unknowns

The prompt distinguishes:

```text
confirmed
hypothesis
unknown
```

Information may come from:

```text
user
provided_context
product_prd
feature_prd
high_level_design
feature_design
existing_adr
existing_rfc
technical_research
codebase
tests
schema
repository_guideline
ai_suggestion
```

`confirmed` means explicitly supported by authoritative context or the user.

`hypothesis` means plausible but not yet confirmed.

`unknown` means material implementation information is still missing.

An AI-generated implementation suggestion must never silently become a confirmed design decision.

## Current Implementation vs. Target Design

The prompt explicitly distinguishes:

```text
current
target
legacy
deprecated
proposed
```

This is important when working with an existing codebase.

For example:

```text
Current:
PaymentService talks directly to Prisma.

Target:
PaymentService depends on PaymentRepository.
```

The existence of the current implementation does not automatically make it the desired future design.

Likewise, an existing test describes current behavior but does not automatically define desired future behavior.

## Stable IDs and Traceability

Recommended prefixes include:

```text
MOD-001
CLS-001
IFACE-001
DATA-001
ALG-001
SEQ-001
STATE-001
TX-001
CONC-001
VAL-001
ERR-001
OBS-001
TEST-001
RISK-001
DEC-001
HYP-001
```

These IDs support relationships such as:

```text
CLS-002 implements IFACE-001
```

```text
ALG-001 operates on DATA-002
```

```text
TX-001 protects STATE-001
```

```text
TEST-003 verifies ERR-002
```

The objective is to make implementation, testing, code review, and downstream agent workflows easier to trace.

## Module Decomposition

The prompt may define modules using IDs such as:

```text
MOD-001
MOD-002
```

A module can capture:

```text
Name
Responsibility
Inputs
Outputs
Dependencies
Owned State
Visibility
Status
Source
```

The objective is cohesion, not maximum fragmentation.

The prompt should avoid introducing unnecessary layers or abstractions.

## Classes, Services, and Internal Interfaces

The LLD may define:

```text
CLS-001
IFACE-001
```

Possible implementation kinds may include:

```text
class
service
repository
adapter
handler
controller
worker
factory
strategy
interface
function_module
```

These are examples, not mandatory patterns.

A type may capture:

```text
Name
Kind
Responsibility
Methods
Inputs
Outputs
Dependencies
Lifecycle
Visibility
Implemented Interfaces
Status
Source
```

The prompt should not force object-oriented design into a codebase that uses another paradigm.

## Data Structures and Internal Schemas

The LLD may distinguish:

```text
external contract
internal DTO
domain object
persistence model
cache representation
event representation
```

This separation helps avoid accidental coupling between layers.

A data structure may capture:

```text
Name
Purpose
Fields
Types
Constraints
Ownership
Mutability
Serialization
Persistence
Status
Source
```

Field-level detail should be included when it materially affects implementation.

## Algorithms and Decision Logic

Use algorithm IDs such as:

```text
ALG-001
ALG-002
```

Only non-trivial logic needs explicit design.

An algorithm may capture:

```text
Purpose
Inputs
Outputs
Preconditions
Steps
Complexity
Failure Conditions
Determinism
Status
Source
```

The prompt should avoid documenting trivial control flow merely to make the LLD longer.

## Detailed Call Sequences

Use sequence IDs such as:

```text
SEQ-001
SEQ-002
```

Call sequences may capture:

```text
Trigger
Caller
Callee
Method or Operation
Order
Data Passed
State Change
Failure Path
Related Upstream Flow
Status
Source
```

Sequence diagrams are optional.

They should be used only when they improve understanding.

## State and State Transitions

Stateful implementations may use IDs such as:

```text
STATE-001
STATE-002
```

A state transition may capture:

```text
State
Allowed Transition
Trigger
Guard Condition
Side Effect
Invalid Transition
Persistence
Status
Source
```

The prompt should not force a state-machine abstraction when one is unnecessary.

## Persistence and Transaction Boundaries

Use IDs such as:

```text
TX-001
TX-002
```

A transaction definition may capture:

```text
Operation
Data Written
Transaction Boundary
Isolation Requirement
Atomicity Requirement
Rollback Behavior
Idempotency
Failure Handling
Status
Source
```

Transaction strategy must not be invented.

The prompt should make consistency expectations explicit before choosing implementation mechanics.

## Concurrency and Synchronization

Use IDs such as:

```text
CONC-001
CONC-002
```

Concurrency design may capture:

```text
Concurrent Operation
Shared Resource
Race Condition
Synchronization Strategy
Lock Scope
Conflict Handling
Deadlock Considerations
Status
Source
```

The prompt should not automatically choose:

```text
mutex
distributed lock
optimistic locking
pessimistic locking
```

These are implementation choices that require context.

## Validation and Internal Errors

Validation may use:

```text
VAL-001
VAL-002
```

Internal errors may use:

```text
ERR-001
ERR-002
```

The LLD should preserve externally visible behavior defined by the FDD while making internal behavior explicit.

Validation may capture:

```text
Condition
Layer
Behavior
Related Contract or State
Status
Source
```

Errors may capture:

```text
Condition
Internal Error
Propagation
Mapping
Recovery
Related Upstream Error
Status
Source
```

## Implementation-Level Observability

Use IDs such as:

```text
OBS-001
OBS-002
```

The LLD may define specific instrumentation points such as:

- log locations;
- metric emission points;
- trace spans;
- correlation identifiers;
- timing points;
- failure counters;
- debug attributes.

The prompt should preserve upstream observability requirements and existing project tooling.

It should not invent a vendor or observability stack.

## Security and Sensitive Data

The LLD may define implementation-level security controls such as:

- authorization checks;
- validation;
- sanitization;
- secret handling;
- sensitive-data boundaries;
- audit hooks;
- privilege boundaries;
- data-exposure rules.

The prompt should not introduce security mechanisms not supported by context.

## Testability and Verification

Use stable IDs such as:

```text
TEST-001
TEST-002
```

Possible test types may include:

```text
unit
integration
contract
component
property
concurrency
migration
performance
```

These are examples, not defaults.

A test design entry may capture:

```text
Test Type
Target
Scenario
Dependency Isolation
Expected Behavior
Related IDs
Status
Source
```

The prompt should design testability seams where necessary, but should not generate full test code unless explicitly requested.

## Implementation Risks and Trade-offs

Use stable IDs such as:

```text
RISK-001
RISK-002
```

An implementation risk may capture:

```text
Description
Probability
Impact
Affected Components
Mitigations
Trade-offs
Contingency
Status
Source
```

AI-proposed mitigations must remain hypotheses until confirmed.

## Open Questions, Pending Decisions, and Hypotheses

The workflow explicitly distinguishes:

```text
Open Questions
Pending Decisions
Hypotheses
```

Examples:

```text
Open Question
→ Does the existing database transaction cover both writes?
```

```text
Pending Decision
→ Whether the idempotency key belongs in the domain entity or a dedicated store.
```

```text
Hypothesis
→ Optimistic locking may be sufficient for the expected write contention.
```

The prompt should keep unresolved items visible rather than hiding them in polished prose.

## Handling Feature Design Docs

The FDD is the most direct upstream technical input for the LLD.

The prompt should preserve:

- runtime behavior;
- public contracts;
- error semantics;
- fallback behavior;
- compatibility requirements;
- observability expectations;
- acceptance criteria.

The LLD should refine that behavior into internal implementation structure.

If the LLD cannot satisfy the FDD without changing externally visible behavior, the prompt should surface the conflict and recommend revisiting the upstream design.

## Handling High-Level Designs

The HLD provides architectural constraints.

The LLD should preserve:

- architectural boundaries;
- component ownership;
- approved technologies;
- communication patterns;
- security constraints;
- observability constraints;
- ADR-linked decisions.

The LLD should not silently move responsibility across architectural boundaries.

## Handling ADRs and RFCs

When ADRs or RFCs are available, the prompt should:

- preserve accepted decisions;
- preserve relevant rejected alternatives;
- detect superseded decisions;
- identify implementation consequences;
- surface conflicts;
- reference relevant decisions.

Accepted architectural decisions should not be reopened without a material reason.

## Handling Codebase Context

The codebase may provide evidence about:

- modules;
- packages;
- dependencies;
- interfaces;
- data models;
- persistence;
- error handling;
- logging;
- tests;
- naming;
- architecture patterns.

However:

```text
current code
≠
approved target design
```

The prompt should distinguish observed implementation from desired implementation.

If current code conflicts with authoritative design documentation, the conflict should be surfaced.

## Handling Tests

Existing tests provide evidence about current observable behavior.

They can help identify:

- regression expectations;
- current contracts;
- edge cases;
- test seams;
- undocumented behavior.

However:

```text
existing test
≠
future requirement
```

The prompt should distinguish current coverage from target design.

## Handling Technical Research

Technical research may suggest implementation alternatives.

The prompt should:

- treat research as supporting knowledge;
- preserve useful references;
- distinguish recommendation from decision;
- avoid silently promoting a research option to confirmed implementation.

Research informs design.

Research does not automatically define design.

## Source Traceability

The prompt preserves the source of important implementation information when useful.

Sources may include:

- Product PRD;
- Feature PRD;
- HLD;
- FDD;
- ADR;
- RFC;
- codebase;
- tests;
- schemas;
- technical research;
- project guidelines;
- user confirmation.

References can be consolidated in the final `References` section when detailed inline provenance would reduce readability.

## Consistency Checks

Before generating the final LLD, the prompt checks questions such as:

- Does the design satisfy Feature PRD requirements?
- Does it preserve HLD boundaries?
- Does it preserve FDD contracts and behavior?
- Are ADR and RFC decisions respected?
- Is current code distinguished from target design?
- Are modules cohesive?
- Do responsibilities overlap unnecessarily?
- Are dependency directions coherent?
- Are interfaces clearly owned?
- Are internal and external data models accidentally coupled?
- Do algorithms preserve required invariants?
- Do call sequences match the feature behavior?
- Are state transitions valid?
- Do transactions preserve required consistency?
- Are concurrency risks handled where needed?
- Are validation rules intentionally placed?
- Do internal errors map correctly to upstream behavior?
- Do observability hooks satisfy the FDD?
- Is sensitive data protected?
- Are critical behaviors testable?
- Were patterns or technologies invented?
- Were numeric values invented?
- Are AI suggestions still hypotheses?
- Has the document accidentally become production code or an implementation task list?

When a material inconsistency prevents a reliable LLD, the prompt should return to the relevant stage rather than generate a misleading document.

## Expected Output

The primary output is a Low-Level Design in Markdown.

Depending on the implementation, the document may contain:

```text
Document Information
Implementation Context
Upstream References
Module Decomposition
Classes, Services, and Interfaces
Data Structures
Algorithms and Decision Logic
Detailed Call Sequences
State and State Transitions
Persistence and Transactions
Concurrency and Synchronization
Validation and Internal Errors
Observability Hooks
Security and Sensitive Data
Testability and Verification
Implementation Risks and Trade-offs
Open Questions
Pending Decisions
Hypotheses
References
```

Sections that do not add value should be omitted.

The prompt should not create empty sections simply because the template supports them.

## Optional JSON Output

After generating the Markdown LLD, the prompt can optionally generate a structured JSON representation.

The JSON is intended for:

- programmatic consumption;
- automation;
- AI agent workflows;
- implementation planning;
- test planning;
- design validation;
- code-generation context;
- downstream tooling.

The Markdown and JSON outputs must represent the same design state.

They should not become two independent sources of truth.

Conceptually:

```text
implementation-design state
        ├── Markdown → human-readable representation
        └── JSON     → structured representation
```

## Example Usage

A minimal invocation might be:

```text
Create an LLD for the feature described in the attached FDD.
```

A richer invocation might be:

```text
Create an LLD for the attached Feature Design Doc.

Use the HLD, ADRs, repository guidelines, current code, schemas, and tests as context.

Do not invent patterns, transaction behavior, synchronization strategies, dependencies, or numeric values.

Ask me only for implementation decisions that are materially missing.
```

Another example:

```text
Review the FDD, codebase, and existing tests.

Help me define the target Low-Level Design.

Identify conflicts between current code and the intended feature behavior before generating the final document.
```

## Known Limitations

The quality of the LLD depends on the available implementation context.

The prompt cannot independently verify:

- whether code examples are complete;
- whether the repository is current;
- undocumented project conventions;
- hidden runtime behavior;
- real production contention;
- database isolation behavior not present in context;
- infrastructure constraints not provided;
- whether tests accurately capture production behavior;
- whether a proposed algorithm meets real performance requirements;
- whether a transaction strategy is supported by infrastructure;
- whether concurrency assumptions are realistic;
- whether an upstream FDD is correct;
- whether an ADR has been superseded outside the provided context.

A polished LLD is not proof that the implementation design is correct.

AI-assisted low-level design should not replace appropriate validation with:

- senior engineers;
- software architects;
- maintainers;
- database specialists;
- security teams;
- platform teams;
- SRE or operations;
- domain experts;
- affected consumer teams.

The prompt can expose uncertainty and compare alternatives, but it cannot authoritatively resolve missing project decisions without authoritative input.

## Tested Models

Not formally evaluated yet.

When this prompt is tested systematically, record models and observations here.

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

- a trivial change that may not justify an LLD;
- an implementation with complete FDD and codebase context;
- an implementation with only an FDD;
- an FDD that conflicts with current code;
- an HLD that conflicts with the proposed internal structure;
- an ADR that constrains implementation choices;
- existing code that should not become target design automatically;
- tests that describe legacy behavior;
- a transaction boundary that remains unknown;
- a concurrency strategy that remains unknown;
- an AI-suggested design pattern that must remain a hypothesis;
- ambiguous ownership between modules;
- duplicated DTO / domain / persistence representations;
- non-trivial algorithm design;
- state-machine behavior;
- internal errors that must preserve FDD-visible behavior;
- insufficient testability;
- an LLD that drifts into production code;
- an LLD that drifts into implementation-task planning;
- a request to generate a partial LLD before all stages are complete.

Useful evaluation criteria may include:

- instruction adherence;
- context-first behavior;
- one-primary-question-per-turn compliance;
- per-stage confirmation compliance;
- implementation-invention rate;
- hypothesis-labeling accuracy;
- source-tracking accuracy;
- stable-ID consistency;
- module-cohesion quality;
- interface ownership clarity;
- dependency-direction clarity;
- data-ownership clarity;
- current-vs-target distinction accuracy;
- algorithm completeness;
- transaction-boundary clarity;
- concurrency-analysis quality;
- error-mapping correctness;
- observability-hook completeness;
- testability quality;
- upstream-design preservation;
- FDD-vs-LLD boundary compliance;
- LLD-vs-code boundary compliance;
- LLD-vs-implementation-plan boundary compliance;
- Markdown format compliance;
- JSON validity;
- semantic consistency between Markdown and JSON;
- interview efficiency;
- unnecessary-question rate;
- overall LLD usefulness.

Pairwise evaluation may also be useful when comparing future versions of this prompt.

## Maintenance

When changing `prompt.md`, consider updating this document if the change affects:

- interview workflow;
- confirmation behavior;
- implementation scope;
- inputs;
- status or source rules;
- stable IDs;
- module decomposition;
- class/interface modeling;
- data structure modeling;
- algorithms;
- call sequences;
- state handling;
- transaction handling;
- concurrency handling;
- validation or error behavior;
- observability;
- security;
- testability;
- FDD/HLD/LLD boundaries;
- LLD/implementation-plan boundaries;
- output format;
- consistency checks;
- optional JSON behavior;
- known limitations;
- recommended usage.

Git remains the source of truth for the complete history.

This README should provide a concise human-readable view of the prompt's current behavior.

## Changelog

### 2026-10-16

Initial version.

- Added a context-first Low-Level Design workflow.
- Added reuse of Product PRDs, Feature PRDs, HLDs, FDDs, ADRs, RFCs, research, codebase context, schemas, tests, and project conventions.
- Added one-primary-question-per-turn behavior.
- Added mandatory confirmation after every LLD interview stage.
- Added explicit handling of confirmed information, hypotheses, and unknowns.
- Added source tracking for implementation information.
- Added stable IDs for modules, classes, interfaces, data structures, algorithms, sequences, state, transactions, concurrency, validation, errors, observability, tests, risks, decisions, and hypotheses.
- Added explicit current-vs-target implementation handling.
- Added safeguards against silent implementation decisions.
- Removed generic pattern, technology, synchronization, and numeric defaults.
- Added module and component decomposition.
- Added class, service, and internal-interface modeling.
- Added internal data-structure and schema modeling.
- Added algorithm and decision-logic modeling.
- Added detailed call-sequence modeling.
- Added state-transition modeling.
- Added persistence and transaction-boundary modeling.
- Added concurrency and synchronization analysis.
- Added validation and internal-error modeling.
- Added implementation-level observability hooks.
- Added security and sensitive-data handling.
- Added testability and verification strategy.
- Added implementation risk and trade-off tracking.
- Added open-question, pending-decision, and hypothesis handling.
- Added explicit FDD / LLD / implementation-plan boundaries.
- Added consistency checks before final document generation.
- Added source traceability and references.
- Added Markdown output with optional structured JSON representation.

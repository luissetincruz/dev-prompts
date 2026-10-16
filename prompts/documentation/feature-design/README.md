# Feature Design

Reusable context-aware prompt for creating clear, technically actionable, and traceable Feature Design Docs (FDDs).

The prompt helps the user define the technical behavior of a specific feature by reusing existing project context, interviewing only where information is missing, distinguishing confirmed decisions from hypotheses, and producing a maintainable FDD for humans and AI-assisted implementation workflows.

## Prompt

[View the raw prompt](./prompt.md)

## Objective

The purpose of this prompt is to transform product requirements, architectural context, existing contracts, technical research, and codebase evidence into a detailed feature-level technical design.

It is designed to:

- understand the technical motivation of a feature;
- reuse existing project context before asking questions;
- preserve confirmed PRD and HLD constraints;
- define technical objectives and invariants;
- define feature scope and exclusions;
- describe detailed runtime flows;
- define public and externally relevant contracts;
- distinguish current contracts from target contracts;
- specify error, exception, fallback, and resilience behavior;
- define observability requirements;
- identify dependencies and compatibility requirements;
- define traceable technical acceptance criteria;
- identify technical risks and mitigations;
- preserve relevant ADRs, RFCs, research, and references;
- make uncertainty explicit;
- generate a structured FDD in Markdown;
- optionally provide the same information as structured JSON.

The goal is not to produce the largest possible technical document.

The goal is to produce the smallest FDD that reliably communicates the feature's runtime behavior, contracts, failure semantics, compatibility requirements, acceptance conditions, and unresolved technical decisions.

## When to Use

Use this prompt when a feature has enough technical complexity that implementation would otherwise depend on assumptions or undocumented behavior.

Typical cases include work involving:

- a new public API;
- changes to an existing API contract;
- new events or queue contracts;
- SDK changes;
- configuration changes;
- new error semantics;
- fallback behavior;
- retry or timeout policies;
- new observability requirements;
- backward-compatibility concerns;
- breaking changes;
- migrations;
- security-sensitive behavior;
- performance-sensitive behavior;
- distributed state;
- concurrency;
- persistence behavior;
- integration with external systems;
- multiple consumers;
- complex rollout constraints;
- technical acceptance criteria that need explicit definition.

Examples include:

```text
Create an FDD for a distributed rate-limiting feature that exposes HTTP headers and supports multiple storage backends.
```

```text
Help me define the Feature Design for adding idempotent payment processing to an existing checkout platform.
```

```text
Create an FDD for a new event contract that must remain backward-compatible with existing consumers during rollout.
```

The prompt is also useful when technical information already exists across:

- Feature PRDs;
- PRDs;
- HLDs;
- ADRs;
- RFCs;
- API specifications;
- event contracts;
- queue contracts;
- SDK documentation;
- Deep Research;
- repository documentation;
- existing code;
- tests;
- engineering guidelines.

In those cases, the prompt should extract what is already known, identify conflicts, and ask only about material feature-design gaps.

## When Not to Use

This prompt is usually unnecessary for:

- trivial code changes;
- internal refactors with no contract impact;
- small UI changes with no technical ambiguity;
- routine bug fixes;
- dependency patch upgrades;
- implementation tasks already fully defined by an existing FDD;
- system-wide architectural design;
- business requirements definition;
- architectural decision rationale;
- operational runbooks;
- direct task breakdowns;
- line-by-line implementation instructions.

Examples that may not justify a dedicated FDD:

```text
Rename one private helper function.
```

```text
Change a log message without changing observable behavior.
```

```text
Upgrade a library from one patch version to another with no compatibility impact.
```

If the requested work appears too small to justify an FDD, the prompt should explain this briefly and allow the user to decide whether to continue.

For product requirements, use a Feature PRD.

For system-wide architecture, use a High-Level Design.

For architectural decision rationale, use an ADR.

For proposals requiring broader technical discussion, use an RFC.

For class-level or implementation-level design, use an LLD or implementation plan.

## Expected Inputs

The prompt can work with one or more of the following:

- a Feature PRD;
- a PRD;
- a High-Level Design;
- architecture documentation;
- ADRs;
- RFCs;
- technical research;
- Deep Research reports;
- API specifications;
- event contracts;
- queue contracts;
- SDK documentation;
- database documentation;
- repository guidelines;
- engineering guidelines;
- infrastructure documentation;
- deployment documentation;
- existing source code;
- repository structure;
- existing interfaces;
- existing tests;
- issue or ticket descriptions;
- operational constraints;
- performance requirements;
- availability requirements;
- security constraints;
- compliance requirements;
- stakeholder notes.

A complete technical design does not need to exist before using the prompt.

The prompt is designed to reuse existing information first and then guide the user through the missing feature-level technical decisions.

The quality of the resulting FDD depends on the quality, authority, and completeness of the available context.

## Project Context

This is a generic reusable prompt.

It does not contain assumptions about a specific:

- company;
- repository;
- programming language;
- framework;
- database;
- message broker;
- cloud provider;
- deployment platform;
- API style;
- retry policy;
- timeout value;
- error code;
- status code;
- security model;
- observability stack;
- business domain.

Project-specific knowledge should remain in the project that owns it.

When project context is available, combine this prompt with artifacts such as:

```text
AGENTS.md
```

```text
CLAUDE.md
```

```text
Feature PRDs
```

```text
High-Level Designs
```

```text
ADRs
```

```text
RFCs
```

```text
technical research
```

```text
API specifications
```

```text
repository documentation
```

```text
existing contracts
```

```text
tests
```

```text
existing code
```

Conceptually:

```text
generic Feature Design prompt
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

The prompt should use existing context before asking the user to repeat information.

## Context-First Workflow

The prompt is intentionally context-first rather than interview-first.

Before asking questions, it should inspect available context and identify:

- feature requirements;
- confirmed HLD decisions;
- accepted ADRs and RFCs;
- existing public contracts;
- technical research;
- codebase behavior;
- existing tests;
- compatibility constraints;
- contradictions;
- missing information.

Conceptually:

```text
existing context
        ↓
feature-design extraction
        ↓
gap detection
        ↓
targeted interview
        ↓
consistency check
        ↓
Feature Design Doc
```

The interview exists to fill material gaps rather than rediscover information that is already documented.

## Interview Workflow

The prompt follows a structured feature-design workflow.

The main sequence is:

```text
analyze existing context
        ↓
technical context and motivation
        ↓
technical objectives and invariants
        ↓
scope and exclusions
        ↓
detailed flows and diagrams
        ↓
public and externally relevant contracts
        ↓
errors, exceptions, fallback, and resilience
        ↓
observability
        ↓
dependencies and compatibility
        ↓
technical acceptance criteria
        ↓
technical risks and mitigations
        ↓
open questions, pending decisions, and hypotheses
        ↓
consistency check
        ↓
final confirmation
        ↓
Feature Design Doc
```

The interview asks one primary question at a time.

The prompt deliberately requires confirmation at the end of every interview stage.

Each stage should end with:

- a concise summary;
- remaining ambiguity, hypotheses, open questions, or pending decisions;
- a request for confirmation or correction.

The next stage should not begin until the user confirms or corrects the current one.

This creates an explicit review checkpoint throughout the feature-design process.

## Interview Confirmation Model

Every interview stage follows this pattern:

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

If a stage is already fully supported by authoritative project context, the prompt should still summarize what it extracted and ask the user to confirm that interpretation.

If the user corrects a previously confirmed stage, the prompt should:

- update the current technical state;
- reconsider dependent flows;
- reconsider contracts;
- reconsider error behavior;
- reconsider acceptance criteria;
- reconsider compatibility;
- explain the impact when necessary;
- reconfirm affected stages.

## Feature Design Elicitation Principles

### Existing Context First

The prompt should inspect available project information before asking questions.

If a technical fact is already clearly supported by authoritative context, it should be reused rather than asked again.

### No Silent Technical Decisions

The prompt must not silently choose:

- endpoints;
- payloads;
- headers;
- status codes;
- event schemas;
- SDK signatures;
- retry counts;
- timeout values;
- backoff policies;
- rate limits;
- fallback policies;
- dependency versions;
- observability vendors;
- compatibility strategies;
- persistence approaches;
- performance targets.

Missing information should result in:

- a question;
- an explicit unknown;
- an open decision;
- a pending decision;
- or an AI suggestion clearly marked as a hypothesis.

### No Generic Technical Defaults

The prompt must not assume common technologies or numeric values simply because they are popular.

For example, it should not automatically assume:

```text
REST
gRPC
Kafka
RabbitMQ
Redis
PostgreSQL
HTTP 429
3 retries
exponential backoff
2 second timeout
Prometheus
OpenTelemetry
99.9% availability
10 ms latency
1 MB payload
```

These may be valid in a specific project, but they are not universal defaults.

### Preserve Corrections

When the user changes or corrects a previously collected technical fact, the prompt should:

- replace obsolete information;
- use the corrected value going forward;
- re-evaluate dependent flows, contracts, errors, risks, and acceptance criteria;
- reconfirm affected stages when necessary.

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
feature_prd
prd
high_level_design
existing_adr
existing_rfc
technical_research
api_spec
event_contract
codebase
tests
ai_suggestion
```

`confirmed` means the information is explicitly supported by the user or authoritative project context.

`hypothesis` means the information may be reasonable but has not yet been confirmed.

`unknown` means the information is still missing.

An AI-generated suggestion must never silently become confirmed feature behavior.

For example:

```text
Timeout:
2 seconds

Status:
hypothesis

Source:
ai_suggestion
```

must remain provisional until the user confirms, changes, or rejects it.

This distinction is especially important when the FDD will later be consumed by implementation agents.

## Stable IDs and Traceability

The prompt uses stable IDs when they improve cross-reference and implementation traceability.

Recommended prefixes include:

```text
OBJ-001
FLOW-001
CONTRACT-001
ERR-001
OBS-001
DEP-001
AC-001
RISK-001
DEC-001
HYP-001
```

These IDs allow relationships such as:

```text
CONTRACT-001
→ verified by AC-002
```

```text
ERR-003
→ occurs in FLOW-001
```

```text
DEP-002
→ required by CONTRACT-004
```

The objective is to make technical requirements, behavior, validation, and risks easier to connect across implementation and testing workflows.

## Technical Objectives and Invariants

The prompt identifies technical outcomes and guarantees that the feature must preserve.

Examples may include:

- deterministic behavior;
- idempotency;
- atomicity;
- latency;
- throughput;
- consistency;
- compatibility;
- security guarantees;
- resilience guarantees;
- resource limits;
- observability expectations.

Numeric targets must not be invented.

Where appropriate, the prompt should prefer explicit invariants over vague statements.

Example:

```text
At most one state transition may be committed for a given operation ID.
```

is stronger than:

```text
Duplicate updates should be avoided.
```

## Scope and Exclusions

The FDD defines the feature's technical boundary.

The prompt separates:

```text
Included
Excluded
```

This can clarify:

- behavior implemented now;
- behavior delegated to another component;
- integrations included;
- algorithms or strategies excluded;
- migration work excluded;
- future extensions;
- operational tooling outside the current feature.

The prompt should not silently expand the feature.

## Detailed Flows

The prompt uses stable flow IDs such as:

```text
FLOW-001
FLOW-002
```

A flow may capture:

```text
Name
Trigger
Preconditions
Steps
Validations
Persistence
Cache interaction
External calls
Events
Outcome
Failure points
Related contracts
Status
Source
```

Depending on the feature, the FDD may contain:

- main flows;
- alternative flows;
- error flows;
- fallback flows;
- recovery flows.

Diagrams may be used when they improve understanding.

They are not required merely because the document supports them.

## Public Contracts

The prompt defines public or cross-component contracts in enough detail for integration.

Contract types may include:

```text
function
method
http_endpoint
queue
stream
event
sdk
cli
webhook
file_contract
```

A contract may capture:

```text
Name
Type
Change Type
Signature or Route
Method
Protocol
Request
Response
Headers
Status semantics
Event semantics
Limits
Timeout behavior
Versioning
Compatibility
Consumers
Status
Source
```

The prompt should distinguish current behavior from target behavior.

## Contract Change Classification

Contracts are classified when relevant as:

```text
existing
new
modified
deprecated
removed
proposed
```

### Existing

The contract already exists and is expected to remain unchanged.

### New

A confirmed new contract will be introduced.

### Modified

An existing contract changes its target behavior.

### Deprecated

The contract remains temporarily supported but should no longer be adopted.

### Removed

The contract will no longer be supported.

### Proposed

The contract is under consideration but has not yet been confirmed.

This classification helps make compatibility and rollout implications explicit.

## Errors, Exceptions, Fallback, and Resilience

The prompt uses stable error IDs such as:

```text
ERR-001
ERR-002
```

A failure definition may capture:

```text
Condition
Observable behavior
Treatment
Retryable
Timeout behavior
Fallback
Status or error mapping
Invariant
Status
Source
```

Relevant failure modes may include:

- validation failure;
- dependency timeout;
- dependency unavailable;
- malformed response;
- concurrency conflict;
- partial failure;
- stale data;
- rate limit;
- retry exhaustion;
- circuit open;
- degraded operation.

Resilience patterns such as retries, backoff, circuit breakers, bulkheads, fallback, idempotency, or deduplication are not automatic defaults.

They should only be included when supported by context or explicitly confirmed.

## Observability

The FDD defines what must be observable to verify and operate the feature.

Relevant areas may include:

- metrics;
- structured logs;
- log fields;
- tracing spans;
- tracing attributes;
- sampling;
- cardinality concerns;
- correlation identifiers;
- dashboards;
- alerts;
- sensitive-data protections.

The prompt should focus first on:

```text
what must be observable
```

and preserve the project's existing observability stack when one exists.

It should not invent a vendor or tool.

## Dependencies and Compatibility

The prompt identifies dependencies and their compatibility requirements.

A dependency may capture:

```text
Component
Purpose
Minimum Version
Maximum Version
Compatibility Notes
Required or Optional
Status
Source
```

Dependency versions must not be invented.

Compatibility analysis may include:

- backward compatibility;
- forward compatibility;
- breaking changes;
- deprecations;
- migration requirements;
- rollout order;
- mixed-version operation;
- API versioning;
- event-schema versioning;
- SDK versioning;
- storage-format compatibility.

This is particularly important for distributed systems and rolling deployments.

## Technical Acceptance Criteria

The prompt uses stable acceptance-criterion IDs such as:

```text
AC-001
AC-002
```

Acceptance criteria should be:

- observable;
- testable when practical;
- unambiguous;
- related to one or more technical elements.

Relationships may include:

```text
AC-001
→ verifies CONTRACT-001
```

```text
AC-002
→ verifies FLOW-001
```

```text
AC-003
→ verifies ERR-002
```

This creates a direct path from design to implementation validation.

## Risks and Mitigations

The prompt uses stable IDs such as:

```text
RISK-001
RISK-002
```

A risk may contain:

```text
Description
Probability
Impact
Mitigations
Contingency Plan
Related Flow or Contract
Status
Source
```

Mitigations may contain multiple actions.

AI-proposed mitigations must remain hypotheses until confirmed.

The prompt should avoid generic risks that do not materially affect the feature.

## Open Questions, Pending Decisions, and Hypotheses

The workflow explicitly distinguishes:

```text
Open Questions
Pending Decisions
Hypotheses
```

An open question is information that is still unknown.

A pending decision is a known technical choice that has not yet been resolved.

A hypothesis is a plausible assumption or AI suggestion that still requires validation.

If a pending decision is architectural in nature, the prompt should recommend revisiting the HLD or creating an ADR/RFC when appropriate.

## Upstream Document Boundaries

The prompt treats upstream artifacts as authoritative context while still detecting contradictions.

Conceptually:

```text
Feature PRD
→ product intent and requirements

High-Level Design
→ architectural boundaries and system-level decisions

Feature Design Doc
→ detailed feature behavior, contracts, compatibility, and validation

Implementation plan / LLD
→ code-level execution detail
```

The FDD should refine the HLD rather than silently replace it.

If detailed feature analysis reveals that an upstream decision is impossible, unsafe, or inconsistent with current requirements, the prompt should surface the conflict rather than silently work around it.

## Handling Feature PRDs and PRDs

When a Feature PRD or PRD is provided, the prompt should use it to understand:

- product intent;
- scope;
- requirements;
- constraints;
- acceptance conditions.

The FDD should not rewrite the full business narrative.

Instead, it should extract only the information that materially affects feature-level technical design.

The FDD should implement confirmed product intent rather than redefine it.

## Handling High-Level Designs

When an HLD is provided, the prompt should:

- preserve confirmed architectural boundaries;
- preserve component ownership;
- preserve confirmed technologies and protocols;
- preserve known security constraints;
- preserve observability requirements;
- preserve accepted architectural decisions;
- identify feature-level details that are still missing.

If the FDD reveals a contradiction with the HLD, the prompt should surface it explicitly.

It should not silently bypass the architecture.

## Handling ADRs and RFCs

When ADRs or RFCs are provided, the prompt should:

- preserve accepted technical decisions;
- preserve relevant rejected alternatives;
- detect superseded decisions;
- surface conflicts between current feature requirements and existing decisions;
- reference relevant ADRs or RFCs in the final FDD.

An accepted ADR should not be reopened silently.

## Handling Technical Research

Technical research and Deep Research can provide useful implementation context.

However:

```text
research option
≠
project decision
```

The prompt should:

- use research as supporting knowledge;
- preserve useful references;
- expose relevant alternatives;
- distinguish recommendations from approved design;
- avoid silently promoting research findings to confirmed feature behavior.

Research informs design.

Research does not automatically define design.

## Handling Existing Contracts

When existing APIs, events, queues, SDKs, or other public contracts are available, the prompt should:

- identify current behavior;
- identify target behavior;
- classify the change;
- identify affected consumers;
- preserve compatibility requirements;
- identify migrations;
- identify rollout implications;
- surface breaking changes explicitly.

Existing behavior is evidence.

It is not automatically the desired future behavior.

## Handling Codebase Context

Existing code can provide evidence about:

- current contracts;
- error-handling conventions;
- configuration patterns;
- dependency versions;
- observability conventions;
- persistence abstractions;
- storage approaches;
- compatibility behavior.

However:

```text
existing implementation
≠
approved target design
```

The prompt should distinguish what exists today from what the feature should become.

If code conflicts with authoritative design documentation, the conflict should be surfaced.

## Handling Tests

Existing tests can provide evidence of current observable behavior.

The prompt may use them to:

- understand regression expectations;
- identify current contracts;
- identify compatibility assumptions;
- identify missing validation for new flows;
- identify behavior that will intentionally change.

Existing tests are evidence of current behavior.

They do not automatically define the desired future design.

## Source Traceability

The prompt preserves the source of important technical information when useful.

Sources may include:

- Feature PRDs;
- HLDs;
- ADRs;
- RFCs;
- API specifications;
- technical research;
- repository documentation;
- codebase context;
- tests;
- user confirmation.

When detailed grounding would make the FDD hard to read, references can be consolidated in the final `References` section.

The objective is to preserve useful provenance without turning the FDD into an unreadable citation log.

## Consistency Checks

Before generating the final FDD, the prompt performs a consistency review.

It checks questions such as:

- Does the feature align with upstream product requirements?
- Does the FDD remain consistent with the HLD?
- Are ADR and RFC decisions preserved?
- Were numeric targets invented?
- Do scope boundaries conflict?
- Are runtime flows complete enough to understand behavior?
- Do flows align with public contracts?
- Are current and target contracts clearly distinguished?
- Are breaking changes explicit?
- Do request and response examples match contract semantics?
- Are header and status semantics internally consistent?
- Does error behavior match flows and contracts?
- Were resilience strategies added without confirmation?
- Does fallback behavior preserve critical invariants?
- Can observability validate important behavior?
- Is sensitive data protected in logs and traces?
- Were dependency versions invented?
- Are compatibility guarantees explicit?
- Are acceptance criteria observable and traceable?
- Are risks connected to the actual feature?
- Are mitigations still correctly classified?
- Are open questions visible?
- Are pending decisions visible?
- Did research findings silently become project decisions?
- Did current code behavior silently become target behavior?
- Has the document accidentally become an implementation task list or LLD?

When a material problem prevents a reliable FDD, the prompt should return to the relevant stage rather than produce a misleading final document.

## Expected Output

The primary output is a Feature Design Doc in Markdown.

Depending on the available information, the document may contain:

```text
Document Information
Technical Context and Motivation
Related Upstream Requirements
Assumptions and Constraints
Technical Objectives and Invariants
Scope and Exclusions
Detailed Flows and Diagrams
Public Contracts
Errors, Exceptions, Fallback, and Resilience
Observability
Dependencies and Compatibility
Technical Acceptance Criteria
Risks and Mitigations
Open Questions
Pending Decisions
Hypotheses
References
```

Sections that do not add value should be omitted.

The prompt should not create empty sections simply because the template supports them.

## Optional JSON Output

After generating the Markdown FDD, the prompt can optionally generate a structured JSON representation.

The JSON is intended for:

- programmatic consumption;
- automation;
- agent workflows;
- validation;
- implementation planning;
- test generation;
- downstream tooling;
- structured context exchange.

The Markdown and JSON outputs must represent the same feature-design state.

They should not become two independent interpretations of the design.

Conceptually:

```text
feature-design state
        ├── Markdown → human-readable representation
        └── JSON     → structured representation
```

If both artifacts are stored in a project, teams should avoid maintaining them independently as separate sources of truth.

## Example Usage

A user may start with minimal context:

```text
I need an FDD for adding idempotent payment processing to our checkout service.
```

The prompt should inspect available context and begin the feature-design interview.

A richer invocation might be:

```text
Create an FDD for the feature described in the attached Feature PRD.

Use the current HLD, ADRs, API specification, Deep Research, and relevant code as context.

Do not invent timeouts, retries, status codes, dependency versions, or numeric targets.

Ask me only for technical information that is materially missing.
```

Another example:

```text
Review the existing API contract, tests, HLD, and implementation.

Help me define the target Feature Design.

Identify breaking changes and contradictions between current behavior and documented architecture before generating the final FDD.
```

The exact invocation depends on the AI tool and available context.

## Known Limitations

The quality of the FDD depends on the information available to the model.

The prompt cannot independently verify:

- undocumented business constraints;
- stakeholder agreement;
- production behavior not present in context;
- hidden infrastructure limitations;
- whether an HLD is still valid;
- whether an ADR has been superseded outside the provided context;
- whether current code reflects intended behavior;
- whether existing tests are complete;
- whether external API documentation is current;
- whether a proposed contract is acceptable to every consumer;
- whether a technical research source is correct;
- whether performance targets are achievable;
- whether a migration plan is operationally safe;
- whether a proposed fallback is acceptable in production.

A polished FDD is not proof that the feature design is correct.

AI-assisted feature design should not replace appropriate validation with:

- senior engineers;
- software architects;
- platform teams;
- API owners;
- security teams;
- infrastructure teams;
- SRE or operations;
- data teams;
- compliance specialists;
- domain experts;
- affected consumer teams.

The prompt can surface uncertainty and alternatives, but it cannot authoritatively resolve missing organizational decisions without authoritative input.

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

- a trivial feature that may not justify an FDD;
- a feature with complete PRD and HLD context;
- a feature with only a high-level requirement;
- a feature with missing timeout or retry decisions;
- an HLD that conflicts with the requested feature behavior;
- an ADR that conflicts with the current codebase;
- technical research that recommends an unapproved technology;
- an AI-suggested default that must remain a hypothesis;
- an existing contract that will be modified;
- a breaking API change;
- a deprecated contract;
- a rollout requiring mixed-version compatibility;
- an event-schema change;
- conflicting tests and documented behavior;
- ambiguous fallback behavior;
- missing observability requirements;
- acceptance criteria that are not traceable to flows or contracts;
- a design that risks descending into LLD or implementation-task detail;
- a request to generate a partial FDD before all stages are complete.

Useful evaluation criteria may include:

- instruction adherence;
- context-first behavior;
- one-primary-question-per-turn compliance;
- per-stage confirmation compliance;
- technical invention rate;
- hypothesis-labeling accuracy;
- source-tracking accuracy;
- stable-ID consistency;
- contract-classification accuracy;
- missing-context detection;
- contradiction detection;
- flow completeness;
- contract completeness;
- error-semantics quality;
- fallback clarity;
- compatibility analysis quality;
- breaking-change detection;
- observability completeness;
- dependency-version invention rate;
- acceptance-criteria traceability;
- architecture-vs-FDD boundary compliance;
- FDD-vs-LLD boundary compliance;
- ADR/RFC preservation;
- reference preservation;
- Markdown format compliance;
- JSON validity;
- semantic consistency between Markdown and JSON;
- interview efficiency;
- unnecessary-question rate;
- overall FDD usefulness.

Pairwise evaluation may also be useful when comparing future versions of this prompt.

## Maintenance

When changing `prompt.md`, consider updating this document if the change affects:

- interview workflow;
- confirmation behavior;
- technical scope;
- inputs;
- status or source rules;
- stable IDs;
- contract change classifications;
- PRD/HLD/FDD boundaries;
- output format;
- consistency checks;
- compatibility handling;
- ADR/RFC handling;
- technical-research handling;
- existing-contract handling;
- codebase handling;
- test handling;
- optional JSON behavior;
- known limitations;
- recommended usage.

Git remains the source of truth for the complete history.

This README should provide a concise human-readable view of the prompt's current behavior.

## Changelog

### 2026-10-16

Initial version.

- Added a context-first Feature Design workflow.
- Added reuse of Feature PRDs, PRDs, HLDs, ADRs, RFCs, research, contracts, codebase context, and tests.
- Added one-primary-question-per-turn behavior.
- Added mandatory confirmation after every feature-design interview stage.
- Added explicit handling of confirmed information, hypotheses, and unknowns.
- Added source tracking for technical information.
- Added stable IDs for objectives, flows, contracts, errors, observability, dependencies, acceptance criteria, risks, decisions, and hypotheses.
- Added safeguards against silent technical decisions.
- Removed generic technical and numeric defaults.
- Added detailed runtime-flow modeling.
- Added public-contract modeling.
- Added contract change classification for existing, new, modified, deprecated, removed, and proposed contracts.
- Added error, exception, fallback, and resilience modeling.
- Added observability requirements.
- Added dependency and compatibility analysis.
- Added technical acceptance-criteria traceability.
- Added technical risk and mitigation tracking.
- Added open-question, pending-decision, and hypothesis handling.
- Added consistency checks before final document generation.
- Added explicit PRD / HLD / FDD / LLD scope boundaries.
- Added handling for Feature PRDs, HLDs, ADRs, RFCs, research, existing contracts, codebase context, and tests.
- Added source traceability and references.
- Added Markdown output with optional structured JSON representation.

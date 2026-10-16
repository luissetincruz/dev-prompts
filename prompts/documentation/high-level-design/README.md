# High-Level Design

Reusable context-aware prompt for creating clear, structured, and technically grounded High-Level Design (HLD) documents.

The prompt helps the user define the architecture of a system, module, or major capability by reusing existing project context, interviewing only where information is missing, distinguishing confirmed decisions from hypotheses, and producing a maintainable HLD for humans and AI-assisted development workflows.

## Prompt

[View the raw prompt](./prompt.md)

## Objective

The purpose of this prompt is to help transform product requirements and technical context into a high-level architectural design before feature-level or implementation-level detail begins.

It is designed to:

- understand the technical objective of the solution;
- reuse existing project context before asking questions;
- identify major architectural boundaries;
- define the overall architecture;
- identify major components and responsibilities;
- describe request and data flows;
- define the high-level data model;
- identify public and externally relevant interfaces;
- capture architecture-driving scalability, availability, resilience, security, and observability concerns;
- preserve existing architectural constraints and decisions;
- distinguish confirmed decisions from proposed options and open decisions;
- identify risks and mitigations;
- preserve relevant ADRs, RFCs, and references;
- make uncertainty explicit;
- generate a structured HLD in Markdown;
- optionally provide the same information as structured JSON.

The goal is not to produce the largest possible architecture document.

The goal is to produce the smallest HLD that reliably communicates the architecture, its boundaries, its important decisions, its unresolved questions, and the context required for more detailed design work.

## When to Use

Use this prompt when a system, module, platform capability, or major feature has enough architectural complexity to justify a dedicated high-level design document.

Typical cases include work involving:

- a new system;
- a major subsystem;
- a new platform capability;
- multiple architectural components;
- communication across service or system boundaries;
- persistent or distributed state;
- new external integrations;
- significant deployment decisions;
- important scalability or availability requirements;
- security boundaries;
- observability requirements;
- major technology or architecture choices;
- multiple teams or technical stakeholders;
- architectural risks;
- downstream Feature Design Docs;
- decisions that may need ADRs or RFCs.

Examples include:

```text
Create an HLD for a centralized rate-limiting capability used by multiple APIs.
```

```text
Help me define the High-Level Design for an enterprise authentication platform with SSO, MFA, and tenant isolation.
```

```text
Create an HLD for a shared event-driven order-processing platform used by checkout, payments, and fulfillment.
```

The prompt is also useful when architectural information already exists across:

- PRDs;
- Feature PRDs;
- ADRs;
- RFCs;
- architecture diagrams;
- project documentation;
- repository documentation;
- technical research;
- Deep Research reports;
- infrastructure documentation;
- code;
- existing API contracts;
- engineering guidelines.

In those cases, the prompt should extract what is already known, identify conflicts, and ask only about material architectural gaps.

## When Not to Use

This prompt is usually unnecessary for:

- trivial code changes;
- small UI adjustments;
- routine bug fixes;
- isolated implementation tasks;
- simple dependency upgrades;
- changes that do not affect architectural boundaries;
- changes already fully covered by an existing HLD;
- detailed endpoint or payload design;
- class-level design;
- algorithm implementation;
- operational runbooks;
- task breakdowns;
- direct code implementation.

Examples that may not justify a dedicated HLD:

```text
Rename one internal function.
```

```text
Add a new optional field to an existing API without changing the architecture.
```

```text
Upgrade a library from one patch version to another.
```

If the requested work appears too small to justify an HLD, the prompt should explain this briefly and allow the user to decide whether to continue.

For detailed feature behavior, use a Feature Design Doc.

For exact API contracts, use an API specification or Feature Design Doc.

For architectural decision rationale, use an ADR.

For proposals requiring broader discussion, use an RFC.

For class-level or implementation-level design, use an LLD or implementation plan.

## Expected Inputs

The prompt can work with one or more of the following:

- a PRD;
- a Feature PRD;
- a problem statement;
- project documentation;
- existing architecture documentation;
- architecture diagrams;
- ADRs;
- RFCs;
- technical research;
- Deep Research reports;
- repository guidelines;
- engineering guidelines;
- infrastructure documentation;
- deployment documentation;
- existing source code;
- repository structure;
- API specifications;
- event or message contracts;
- database documentation;
- operational constraints;
- security constraints;
- compliance requirements;
- performance requirements;
- availability requirements;
- stakeholder notes;
- issue or ticket descriptions.

A complete architecture does not need to exist before using the prompt.

The prompt is designed to reuse existing information first and then guide the user through the missing architectural decisions.

The quality of the resulting HLD depends on the quality, authority, and completeness of the available context.

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
- architecture style;
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
PRDs
```

```text
architecture documentation
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
engineering guidelines
```

```text
infrastructure documentation
```

```text
repository context
```

```text
existing code
```

Conceptually:

```text
generic HLD prompt
        +
product requirements
        +
existing architecture
        +
architectural decisions
        +
technical research
        +
project-specific context
        =
contextualized High-Level Design
```

The prompt should use existing context before asking the user to repeat information.

## Context-First Workflow

The prompt is intentionally context-first rather than interview-first.

Before asking questions, it should inspect available context and identify:

- product requirements;
- current architecture;
- existing constraints;
- confirmed architectural decisions;
- ADRs;
- RFCs;
- technical research;
- relevant codebase context;
- contradictions;
- missing information.

Conceptually:

```text
existing context
        ↓
architecture extraction
        ↓
gap detection
        ↓
targeted interview
        ↓
consistency check
        ↓
High-Level Design
```

The interview exists to fill material gaps rather than rediscover information that is already documented.

## Interview Workflow

The prompt follows a structured architectural-design workflow.

The main sequence is:

```text
analyze existing context
        ↓
context and technical objective
        ↓
architecture overview
        ↓
components and responsibilities
        ↓
request and data flows
        ↓
high-level data model
        ↓
public and externally relevant interfaces
        ↓
scalability, availability, and resilience
        ↓
security
        ↓
observability
        ↓
architectural risks and mitigations
        ↓
ADRs, open questions, pending decisions, and next steps
        ↓
consistency check
        ↓
final confirmation
        ↓
High-Level Design
```

The interview asks one primary question at a time.

Unlike the Feature PRD workflow, this HLD prompt deliberately requires confirmation at the end of every architectural interview stage.

Each stage should end with:

- a concise summary;
- remaining ambiguity or hypotheses;
- a request for confirmation or correction.

The next stage should not begin until the user confirms or corrects the current one.

This creates an explicit review checkpoint throughout the architectural-design process.

## Interview Confirmation Model

Every interview stage follows this pattern:

```text
question
   ↓
user answer or extracted context
   ↓
3–6 line stage summary
   ↓
hypotheses / unknowns
   ↓
user confirmation
   ↓
next stage
```

If a stage is already fully supported by authoritative project context, the prompt should still summarize what it extracted and ask the user to confirm that interpretation.

If the user corrects a previously confirmed stage, the prompt should:

- update the current architectural state;
- reconsider dependent sections;
- explain the impact when necessary;
- reconfirm affected stages.

## Architectural Elicitation Principles

### Existing Context First

The prompt should inspect available project information before asking questions.

If an architectural fact is already clearly supported by authoritative context, it should be reused rather than asked again.

### No Silent Architectural Decisions

The prompt must not silently choose:

- programming languages;
- frameworks;
- databases;
- message brokers;
- cloud providers;
- deployment platforms;
- protocols;
- architecture styles;
- persistence strategies;
- consistency models;
- caching strategies;
- scaling approaches;
- security mechanisms;
- observability stacks;
- availability targets;
- latency targets;
- SLOs;
- SLAs.

Missing information should result in:

- a question;
- an explicit unknown;
- an open decision;
- or an AI suggestion clearly marked as a hypothesis.

### No Generic Architectural Defaults

The prompt must not assume common technologies or values simply because they are popular.

For example, it should not automatically assume:

```text
microservices
REST
gRPC
Kafka
RabbitMQ
Redis
PostgreSQL
Kubernetes
Docker
AWS
RBAC
OAuth
Prometheus
OpenTelemetry
99.9% availability
5 ms latency
```

These may be valid choices in a specific project, but they are not universal defaults.

### Preserve Corrections

When the user changes or corrects a previously collected architectural fact, the prompt should:

- replace obsolete information;
- use the corrected value going forward;
- re-evaluate dependent flows, risks, and decisions;
- reconfirm an affected stage when necessary.

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
existing_architecture
existing_adr
existing_rfc
technical_research
codebase
ai_suggestion
```

`confirmed` means the information is explicitly supported by the user or authoritative project context.

`hypothesis` means the information may be reasonable but has not yet been confirmed.

`unknown` means the information is still missing.

An AI-generated suggestion must never silently become a confirmed architectural decision.

For example:

```text
Availability target:
99.9%

Status:
hypothesis

Source:
ai_suggestion
```

must remain provisional until the user confirms, changes, or rejects it.

This distinction is particularly important when the HLD will later be consumed by other AI agents.

## Architectural Decision Classification

Major architectural choices are classified separately from their confirmation status.

The prompt uses concepts such as:

```text
existing_constraint
confirmed_decision
proposed_option
open_decision
```

### Existing Constraint

A constraint already imposed on the architecture.

Example:

```text
The platform must deploy to the organization's existing Kubernetes environment.
```

### Confirmed Decision

A decision that has already been explicitly approved.

Example:

```text
Asynchronous order events will use Kafka.
```

### Proposed Option

An option under consideration but not yet approved.

Example:

```text
Redis may be used for distributed low-latency state.
```

### Open Decision

A known architectural choice that still needs resolution.

Example:

```text
The persistence strategy has not yet been selected.
```

The prompt must not present proposed options or open decisions as if they were already part of the architecture.

## HLD and Feature Design Boundaries

The HLD focuses on the system-level technical shape.

It may define:

- major components;
- component responsibilities;
- deployment boundaries;
- top-level technologies;
- major communication patterns;
- high-level interfaces;
- high-level data ownership;
- primary request and data flows;
- architecture-driving quality attributes;
- important failure and resilience behavior.

It should normally avoid:

- complete endpoint payloads;
- field-level schemas;
- class diagrams at implementation detail;
- method-level design;
- detailed error catalogs;
- exact algorithms unless architecturally relevant;
- implementation task breakdowns.

Conceptually:

```text
PRD / Feature PRD
→ what and why

High-Level Design
→ system-level technical how

Feature Design Doc
→ detailed feature behavior and contracts

Low-Level Design / implementation plan
→ implementation-level detail
```

The HLD should complement upstream product documents and provide context for downstream technical-design documents.

## Components and Responsibilities

The prompt identifies the major architectural components.

For each component, it may capture:

```text
Name
Responsibility
Owned data
Internal dependencies
External dependencies
Communication role
Lifecycle or deployment boundary
Status
Source
```

The goal is to make component boundaries and ownership explicit without descending to class-level decomposition.

A strong component model should help answer:

```text
What exists?
What does each component own?
What does each component depend on?
How do the components interact?
```

## Request and Data Flows

The prompt documents important end-to-end flows.

Relevant information may include:

- request origin;
- entry point;
- validation;
- authentication;
- authorization;
- transformations;
- service-to-service calls;
- queues;
- events;
- streams;
- persistence;
- replication;
- caching;
- external integrations;
- response path;
- important failure paths.

Request flow and data flow should be separated when they differ materially.

The purpose is to make the architecture understandable without turning the HLD into line-by-line processing logic.

## High-Level Data Model

The HLD may capture:

- major entities;
- relationships;
- ownership;
- sources of truth;
- synchronization;
- replication;
- caching;
- retention;
- versioning;
- consistency expectations.

Field-level schemas are normally outside the scope of the HLD unless a specific field is architecturally significant.

A useful distinction is:

```text
HLD
→ what data domains exist and who owns them

detailed data design
→ exact fields, indexes, constraints, and schemas
```

## Public and Externally Relevant Interfaces

The prompt identifies interfaces that cross architectural boundaries.

Examples may include:

```text
API
queue
stream
SDK
CLI
webhook
file contract
event contract
external provider interface
```

For each interface, the HLD may capture:

```text
Name
Type
Protocol or format
Exposure
Responsibility
Known consumers
Important service expectations
Status
Source
```

The HLD should keep contracts high-level.

Exact payload schemas and exhaustive error behavior usually belong in an API specification or Feature Design Doc.

## Scalability, Availability, and Resilience

The prompt identifies operational qualities that materially influence the architecture.

Relevant topics may include:

- workload characteristics;
- expected scale;
- horizontal scaling;
- vertical scaling;
- partitioning;
- sharding;
- caching;
- rate limiting;
- backpressure;
- retries;
- circuit breakers;
- replication;
- failover;
- fault isolation;
- recovery;
- availability;
- latency;
- throughput;
- concurrency;
- RTO;
- RPO.

Not every architecture needs all of these mechanisms.

Numeric targets must not be invented.

Unknown values should remain unknown or be offered only as hypotheses.

## Security

The prompt identifies security concerns that influence the architecture.

These may include:

- trust boundaries;
- authentication;
- authorization;
- identity propagation;
- secrets management;
- encryption in transit;
- encryption at rest;
- PII;
- sensitive data;
- tenant isolation;
- auditability;
- compliance requirements;
- external exposure.

The prompt should not assume a particular mechanism such as RBAC, OAuth, OIDC, Vault, mTLS, or KMS unless that mechanism is already required or confirmed.

## Observability

The HLD may define what the system must expose for operational understanding.

Relevant areas include:

- structured logs;
- metrics;
- tracing;
- correlation IDs;
- dashboards;
- alerts;
- SLI inputs;
- SLO monitoring;
- dependency visibility;
- latency visibility;
- throughput visibility;
- error visibility.

The prompt should preserve existing organizational observability standards when they are available.

It should not invent a vendor or tooling stack.

## Architectural Risks

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
Mitigation
Contingency Plan
Status
Source
```

AI-proposed mitigations must remain hypotheses until confirmed.

The prompt should avoid generic risks that do not materially affect the architecture.

## ADRs, RFCs, Open Questions, and Pending Decisions

The HLD workflow explicitly distinguishes:

```text
Existing ADRs
Existing RFCs
Open Questions
Pending Decisions
Candidate ADRs
Candidate RFCs
Next Steps
```

An open question is information that is still unknown.

A pending decision is a known architectural choice that has not yet been resolved.

A candidate ADR is a decision that may deserve a durable architectural record.

A candidate RFC is a proposal that may need broader discussion before a decision is made.

The prompt should not create an ADR or RFC simply because a section exists.

## Source Traceability

The prompt preserves the source of important architectural information when useful.

Sources may include:

- PRDs;
- architecture documents;
- ADRs;
- RFCs;
- technical research;
- Deep Research;
- repository documentation;
- codebase context;
- user confirmation.

When detailed grounding would make the HLD hard to read, references can be consolidated in the final `References` section.

The objective is to preserve useful provenance without turning the HLD into an unreadable citation log.

## Handling PRDs

When a PRD is provided, the prompt should use it to understand:

- product intent;
- scope;
- important constraints;
- non-functional requirements;
- relevant success criteria.

The HLD should not rewrite the complete business narrative.

Instead, it should extract only the information that materially drives architecture.

Conceptually:

```text
Feature PRD
→ why, what, scope, requirements

HLD
→ technical shape required to support those requirements
```

## Handling ADRs and RFCs

When ADRs or RFCs are provided, the prompt should:

- preserve accepted decisions;
- preserve relevant rejected alternatives;
- detect superseded decisions;
- surface conflicts between current requirements and existing decisions;
- reference important ADRs or RFCs in the final HLD.

An accepted ADR should not be reopened silently.

If current requirements make an existing decision questionable, the conflict should be surfaced explicitly.

## Handling Technical Research

Technical research and Deep Research can provide valuable context for architectural design.

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
- distinguish recommendations from approved decisions;
- avoid silently promoting research findings to confirmed architecture.

Research informs architecture.

Research does not automatically define architecture.

## Handling Codebase Context

Existing code can provide evidence about:

- current architectural boundaries;
- technologies in use;
- integration patterns;
- persistence approaches;
- deployment assumptions;
- communication patterns.

However:

```text
existing implementation
≠
approved future architecture
```

The prompt should distinguish what exists today from what should exist after the proposed design.

If code conflicts with authoritative architecture documentation, the conflict should be surfaced.

## Consistency Checks

Before generating the final HLD, the prompt performs a consistency review.

It checks questions such as:

- Does the architecture address the stated technical objective?
- Are decisions correctly classified?
- Did any AI suggestion silently become confirmed?
- Are component responsibilities clear?
- Do component ownership boundaries conflict?
- Are request and data flows understandable?
- Are sources of truth explicit?
- Do interfaces align with component boundaries?
- Were communication protocols invented?
- Do resilience strategies align with known requirements?
- Were numeric targets invented?
- Do security controls align with known trust boundaries?
- Does observability fit the architecture?
- Are risks connected to the actual design?
- Are proposed mitigations still marked appropriately?
- Are open questions visible?
- Are pending decisions visible?
- Are ADRs and RFCs preserved?
- Are useful references preserved?
- Has the document accidentally become an FDD or LLD?

When a material problem prevents a reliable HLD, the prompt should return to the relevant stage rather than produce a misleading final document.

## Expected Output

The primary output is a High-Level Design in Markdown.

Depending on the available information, the document may contain:

```text
Document Information
Technical Objective
Driving Requirements
Related Systems
Architecture Overview
Deployment Environment
Major Technologies
Architectural Patterns and Styles
Components and Responsibilities
Request and Data Flows
High-Level Data Model
Public and Externally Relevant Interfaces
Scalability, Availability, and Resilience
Security
Observability
Architectural Risks and Mitigations
Existing Architectural Decisions
Open Questions
Pending Decisions
ADRs and RFCs
Next Steps
Hypotheses
References
```

Sections that do not add value should be omitted.

The prompt should not create empty sections simply because the template supports them.

## Optional JSON Output

After generating the Markdown HLD, the prompt can optionally generate a structured JSON representation.

The JSON is intended for:

- programmatic consumption;
- automation;
- agent workflows;
- architectural filtering;
- downstream tooling;
- structured context exchange.

The Markdown and JSON outputs must represent the same architectural state.

They should not become two independent interpretations of the architecture.

Conceptually:

```text
architectural state
        ├── Markdown → human-readable representation
        └── JSON     → structured representation
```

If both artifacts are stored in a project, teams should avoid maintaining them independently as separate sources of truth.

## Example Usage

A user may start with minimal context:

```text
I need an HLD for a centralized rate-limiting capability used by several backend services.
```

The prompt should inspect available context and begin the architectural interview.

A richer invocation might be:

```text
Create an HLD for the capability described in the attached Feature PRD.

Use the existing ADRs, repository documentation, and Deep Research as context.

Do not invent technologies or numeric targets.

Ask me only for architectural information that is materially missing.
```

Another example:

```text
Review the current architecture documentation, codebase, PRD, and ADRs.

Help me define the target High-Level Design.

Identify contradictions between the current implementation and documented architecture before generating the final HLD.
```

The exact invocation depends on the AI tool and available context.

## Known Limitations

The quality of the HLD depends on the information available to the model.

The prompt cannot independently verify:

- undocumented business constraints;
- hidden infrastructure limitations;
- stakeholder agreement;
- production behavior not present in context;
- network topology not documented;
- security requirements not provided;
- compliance obligations not provided;
- whether an existing ADR is still valid;
- whether the current codebase reflects intended architecture;
- whether a technical research source is correct;
- whether an operational target is achievable;
- whether a proposed design is economically viable.

A polished HLD is not proof that the architecture is correct.

AI-assisted architectural design should not replace appropriate validation with:

- software architects;
- senior engineers;
- platform teams;
- security teams;
- infrastructure teams;
- SRE or operations;
- data teams;
- compliance specialists;
- domain experts;
- product stakeholders, when relevant.

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

- a trivial change that may not justify an HLD;
- a system with complete architecture context;
- a system with only a PRD;
- an HLD with missing availability or latency targets;
- conflicting ADRs;
- an ADR that conflicts with the current codebase;
- technical research that proposes technologies not approved by the project;
- an AI-suggested architecture option that must remain a hypothesis;
- an unresolved protocol decision;
- ambiguous component ownership;
- conflicting sources of truth;
- an architecture with important security boundaries;
- a design that risks descending into FDD or LLD detail;
- a request to generate a partial HLD before all stages are complete.

Useful evaluation criteria may include:

- instruction adherence;
- context-first behavior;
- one-primary-question-per-turn compliance;
- per-stage confirmation compliance;
- architectural invention rate;
- hypothesis-labeling accuracy;
- source-tracking accuracy;
- decision-classification accuracy;
- missing-context detection;
- contradiction detection;
- component-boundary clarity;
- flow completeness;
- data-ownership clarity;
- interface abstraction quality;
- architecture-vs-FDD boundary compliance;
- numeric-target invention rate;
- ADR/RFC preservation;
- reference preservation;
- Markdown format compliance;
- JSON validity;
- semantic consistency between Markdown and JSON;
- interview efficiency;
- unnecessary-question rate;
- overall HLD usefulness.

Pairwise evaluation may also be useful when comparing future versions of this prompt.

## Maintenance

When changing `prompt.md`, consider updating this document if the change affects:

- interview workflow;
- confirmation behavior;
- architectural scope;
- inputs;
- status or source rules;
- decision classifications;
- HLD/FDD boundaries;
- output format;
- consistency checks;
- ADR/RFC handling;
- technical-research handling;
- codebase handling;
- optional JSON behavior;
- known limitations;
- recommended usage.

Git remains the source of truth for the complete history.

This README should provide a concise human-readable view of the prompt's current behavior.

## Changelog

### 2026-10-16

Initial version.

- Added a context-first High-Level Design workflow.
- Added reuse of PRDs, architecture documentation, ADRs, RFCs, research, and codebase context.
- Added one-primary-question-per-turn behavior.
- Added mandatory confirmation after every architectural interview stage.
- Added explicit handling of confirmed information, hypotheses, and unknowns.
- Added source tracking for architectural information.
- Added architectural decision classification for constraints, confirmed decisions, proposed options, and open decisions.
- Removed generic architectural and numeric defaults.
- Added safeguards against silent architectural invention.
- Added major-component and responsibility modeling.
- Added request and data-flow elicitation.
- Added high-level data ownership and source-of-truth modeling.
- Added public and externally relevant interface modeling.
- Added scalability, availability, resilience, security, and observability sections.
- Added architectural risk and mitigation tracking.
- Added ADR, RFC, open-question, and pending-decision handling.
- Added consistency checks before final document generation.
- Added explicit HLD vs. FDD/LLD scope boundaries.
- Added source traceability and references.
- Added Markdown output with optional structured JSON representation.

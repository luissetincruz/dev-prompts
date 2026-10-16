# Product PRD

Reusable context-aware prompt for creating clear, strategic, and traceable Product Requirements Documents at the product or major-initiative level.

The prompt helps the user define why a product should exist, which outcomes it should create, who it serves, how success will be measured, what capabilities belong in scope, and which strategic uncertainties still need resolution.

It is intentionally broader than the existing Feature PRD prompt and is designed to act as upstream context for downstream Feature PRDs, High-Level Designs, and related product and engineering artifacts.

## Prompt

[View the raw prompt](./prompt.md)

## Objective

The purpose of this prompt is to help define a product or major product initiative before detailed feature decomposition, architecture, or implementation begins.

It is designed to:

- clarify why the product or initiative should exist;
- reuse existing company, product, market, research, and project context before asking questions;
- identify the current problem or opportunity;
- distinguish evidence from assumptions;
- identify target audiences, users, and stakeholder groups;
- define outcome-oriented product objectives;
- define success metrics and KPIs without inventing targets;
- establish explicit product boundaries;
- define high-level product capabilities;
- preserve strategic constraints and existing decisions;
- identify dependencies;
- define high-level phases and roadmap direction when useful;
- identify stakeholders and governance;
- surface product risks;
- preserve open questions, pending decisions, hypotheses, and references;
- generate a structured Product PRD in Markdown;
- optionally provide the same information as structured JSON.

The goal is not to create the largest possible product document.

The goal is to produce the smallest Product PRD that reliably communicates why the product exists, what outcomes it must achieve, what it includes, how success is measured, which capabilities matter, and which strategic uncertainties still need resolution.

## Product PRD vs. Feature PRD

This prompt is intentionally different from the existing Feature PRD prompt.

Conceptually:

```text
Product PRD
→ product-level why, outcomes, scope, capabilities, KPIs, phases, stakeholders

Feature PRD
→ feature-level why, behavior, requirements, constraints, acceptance criteria
```

A Product PRD may produce multiple downstream Feature PRDs.

For example:

```text
Product PRD
    ↓
CAP-001
    ↓
Feature PRD A

Product PRD
    ↓
CAP-002
    ↓
Feature PRD B
```

The Product PRD should not attempt to fully specify every capability as a feature.

## When to Use

Use this prompt when defining a complete product, product area, or major initiative that requires strategic alignment before feature-level decomposition.

Typical cases include:

- a new software product;
- a new SaaS offering;
- a major product line;
- a large internal platform initiative;
- a new customer-facing capability composed of multiple features;
- a strategic modernization initiative;
- a major market or segment expansion;
- a multi-team product initiative;
- a new platform capability with significant organizational impact;
- a product that requires clear KPIs, phases, dependencies, stakeholders, and risks.

Examples include:

```text
Create a Product PRD for a new B2B customer onboarding platform.
```

```text
Help me define the product-level PRD for an internal AI platform that will support multiple engineering teams.
```

```text
Create a Product PRD for expanding our commerce platform into a new customer segment.
```

The prompt is also useful when product context already exists across:

- company strategy documents;
- product strategy documents;
- product briefs;
- business cases;
- market research;
- customer research;
- analytics;
- KPI reports;
- roadmap documents;
- existing PRDs;
- existing Feature PRDs;
- stakeholder notes;
- meeting notes;
- project documentation.

In those cases, the prompt should extract what is already known, identify contradictions or gaps, and ask only for information that is materially missing.

## When Not to Use

This prompt is usually unnecessary for:

- a single small feature;
- a small UI change;
- a routine bug fix;
- a technical refactor;
- an isolated implementation task;
- a dependency upgrade;
- a feature whose product context is already fully defined;
- detailed feature requirements;
- system architecture design;
- detailed feature technical design;
- architectural decision rationale;
- operational runbooks;
- implementation task breakdowns.

Examples that may not justify a Product PRD:

```text
Add a password visibility toggle to the login form.
```

```text
Add one optional field to an existing API.
```

```text
Upgrade an internal dependency.
```

If the requested work appears too narrow for a Product PRD, the prompt should explain this briefly and allow the user to decide whether to continue.

For a specific feature, use a Feature PRD.

For system-level architecture, use a High-Level Design.

For detailed feature-level technical behavior, use a Feature Design Doc.

For architectural decision rationale, use an ADR.

## Expected Inputs

The prompt can work with one or more of the following:

- a product idea;
- a product brief;
- a company strategy document;
- a product strategy document;
- a business case;
- an opportunity statement;
- market research;
- customer research;
- user interviews;
- analytics;
- KPI reports;
- existing PRDs;
- existing Feature PRDs;
- project documentation;
- roadmap documents;
- stakeholder notes;
- meeting notes;
- research reports;
- competitive analysis;
- support data;
- sales feedback;
- product metrics;
- business constraints;
- regulatory constraints;
- legal constraints;
- budget constraints;
- organizational constraints;
- existing architecture documentation;
- repository documentation;
- existing source code.

A complete product strategy is not required before using the prompt.

The prompt is designed to reuse existing information first and then guide the user through missing product-level decisions and context.

The quality of the resulting Product PRD depends on the quality, authority, and completeness of the available context.

## Project Context

This is a generic reusable prompt.

It does not contain assumptions about a specific:

- company;
- market;
- customer segment;
- business model;
- repository;
- programming language;
- framework;
- database;
- cloud provider;
- architecture;
- delivery process;
- roadmap model;
- KPI target;
- product strategy.

Project-specific knowledge should remain in the project that owns it.

When product or project context is available, combine this prompt with artifacts such as:

```text
company strategy
```

```text
product strategy
```

```text
market research
```

```text
customer research
```

```text
analytics
```

```text
roadmaps
```

```text
existing PRDs
```

```text
stakeholder notes
```

```text
project documentation
```

Conceptually:

```text
generic Product PRD prompt
        +
company / product strategy
        +
research and analytics
        +
existing product context
        +
stakeholder decisions
        =
contextualized Product PRD
```

The prompt should use existing context before asking the user to repeat information.

## Context-First Workflow

The prompt is intentionally context-first rather than interview-first.

Before asking questions, it should inspect available context and identify:

- company or product strategy;
- existing product requirements;
- customer or market evidence;
- metrics and KPIs;
- known scope boundaries;
- roadmap or phase information;
- stakeholders;
- dependencies;
- constraints;
- contradictions;
- missing information.

Conceptually:

```text
existing context
        ↓
product-context extraction
        ↓
gap detection
        ↓
targeted interview
        ↓
consistency check
        ↓
Product PRD
```

The interview exists to fill material gaps rather than rediscover information that is already documented.

## Interview Workflow

The prompt follows a structured product-definition workflow.

The main sequence is:

```text
analyze existing context
        ↓
product vision and purpose
        ↓
context, problem, and opportunity
        ↓
target audiences, users, and personas
        ↓
product objectives and outcomes
        ↓
success metrics and KPIs
        ↓
scope and product boundaries
        ↓
high-level product capabilities
        ↓
strategic constraints and existing decisions
        ↓
dependencies
        ↓
product strategy and phases
        ↓
roadmap direction
        ↓
stakeholders and governance
        ↓
product risks and mitigations
        ↓
open questions, pending decisions, and hypotheses
        ↓
consistency check
        ↓
final confirmation
        ↓
Product PRD
```

The prompt asks one primary question at a time.

It requires confirmation at the end of every interview stage.

Each stage should end with:

- a concise summary;
- remaining ambiguity, hypotheses, open questions, or pending decisions;
- a request for confirmation or correction.

The next stage should not begin until the user confirms or corrects the current one.

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

If a stage is already fully supported by authoritative context, the prompt should still summarize what it extracted and ask the user to confirm that interpretation.

If the user corrects a previously confirmed stage, the prompt should:

- update the current product state;
- reconsider dependent objectives;
- reconsider KPIs;
- reconsider scope;
- reconsider capabilities;
- reconsider phases;
- reconsider stakeholders;
- reconsider risks;
- explain the impact when necessary;
- reconfirm affected stages.

## Product Discovery Principles

### Existing Context First

The prompt should inspect available product information before asking questions.

If a product fact is already clearly supported by authoritative context, it should be reused rather than asked again.

### No Silent Product Invention

The prompt must not silently invent:

- customer problems;
- market opportunities;
- personas;
- business goals;
- product objectives;
- KPIs;
- KPI targets;
- business rules;
- roadmap phases;
- launch dates;
- stakeholders;
- dependencies;
- strategic constraints;
- product capabilities;
- technical decisions.

Missing information should result in:

- a question;
- an explicit unknown;
- an open decision;
- a pending decision;
- or an AI suggestion clearly marked as a hypothesis.

### No Generic Product Defaults

The prompt must not assume common product patterns simply because they are popular.

For example, it should not automatically assume:

```text
MVP
B2B
B2C
SMB
enterprise
18-35 age group
monthly active users
10% growth target
30% conversion target
Q1 launch
three-phase roadmap
product-led growth
mobile-first
freemium
subscription
```

These may be valid in a specific context, but they are not universal defaults.

### Preserve Corrections

When the user changes or corrects a previously collected product fact, the prompt should:

- replace obsolete information;
- use the corrected value going forward;
- re-evaluate dependent sections;
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
strategy_document
product_document
stakeholder_input
customer_research
market_research
analytics
existing_prd
existing_feature_prd
project_documentation
ai_suggestion
```

`confirmed` means the information is explicitly supported by the user or authoritative context.

`hypothesis` means the information may be reasonable but has not yet been confirmed.

`unknown` means the information is still missing.

An AI-generated suggestion must never silently become a confirmed product decision.

For example:

```text
Target:
Increase activation by 10%

Status:
hypothesis

Source:
ai_suggestion
```

must remain provisional until explicitly confirmed, changed, or rejected.

## Stable IDs and Traceability

The prompt uses stable IDs when they improve cross-reference and downstream traceability.

Recommended prefixes include:

```text
AUD-001
OBJ-001
KPI-001
CAP-001
DEC-001
DEP-001
PHASE-001
STK-001
RISK-001
HYP-001
```

These IDs allow relationships such as:

```text
OBJ-001
→ measured by KPI-001
```

```text
CAP-002
→ supports OBJ-001
```

```text
DEP-001
→ blocks PHASE-002
```

The objective is to make product decisions easier to connect to downstream Feature PRDs, HLDs, prioritization, and delivery workflows.

## Product Vision and Purpose

The Product PRD begins by defining why the initiative should exist.

The vision should answer questions such as:

```text
Why should this product exist?
What meaningful outcome is it intended to create?
How does it connect to broader strategy?
```

It should not become a feature list.

If strategic alignment is unknown, the prompt should say so rather than inventing it.

## Context, Problem, Opportunity, and Evidence

The prompt distinguishes between:

```text
Current State
Problem
Opportunity
Evidence
```

This helps avoid confusing a requested solution with the actual underlying problem.

Evidence may come from:

- customer research;
- analytics;
- support data;
- market research;
- sales feedback;
- stakeholder knowledge;
- business cases.

The prompt should distinguish evidence from interpretation and assumption.

## Target Audiences and Personas

The prompt identifies important users, customers, stakeholders, or affected groups.

It may capture:

```text
Audience or Segment
Needs
Pain Points
Relevant Behaviors
Context of Use
Evidence
Status
Source
```

Personas are optional.

The prompt should not create fictional personas merely because a template supports them.

Actual user segments or stakeholder roles are preferable when they are sufficient.

## Product Objectives

The prompt uses stable objective IDs such as:

```text
OBJ-001
OBJ-002
```

Objectives should describe outcomes rather than solutions.

Prefer:

```text
Reduce time required for customers to complete onboarding.
```

over:

```text
Build a new onboarding wizard.
```

An objective may capture:

```text
Objective
Desired Outcome
Business or User Impact
Priority
Status
Source
```

## Metrics, KPIs, and Guardrails

The prompt explicitly distinguishes:

```text
metric
kpi
guardrail_metric
```

A metric is any measurable signal relevant to the product.

A KPI is a strategically important metric used to determine whether the initiative is succeeding.

A guardrail metric is a measure that should not materially degrade while pursuing another objective.

The prompt should not automatically label every metric as a KPI.

A measure may capture:

```text
Name
Type
Definition
Related Objective
Baseline
Target
Measurement Method
Review Cadence
Status
Source
```

Baselines and targets must not be invented.

Unknown values should remain unknown.

## Product Scope and Boundaries

The Product PRD separates:

```text
In Scope
Out of Scope
Future Considerations
```

This distinction prevents future ideas from silently becoming committed scope.

The prompt may clarify:

- markets included;
- customer segments included;
- platforms included;
- business processes included;
- major capabilities included;
- integrations included;
- deliberately excluded areas;
- future possibilities.

Future considerations should not be presented as committed requirements.

## High-Level Product Capabilities

The prompt uses stable capability IDs such as:

```text
CAP-001
CAP-002
```

A capability may capture:

```text
Name
Description
Primary Audience
Related Objectives
Priority
Status
Source
```

Capabilities should remain high-level.

If a capability requires detailed behavior, it should become a candidate Feature PRD rather than expanding indefinitely inside the Product PRD.

Conceptually:

```text
CAP-001
   ↓
Feature PRD
```

## Strategic Constraints and Existing Decisions

The Product PRD may record confirmed product-level constraints such as:

- legal constraints;
- regulatory constraints;
- supported geographies;
- supported platforms;
- required interoperability;
- business-model constraints;
- contractual commitments;
- organizational policies;
- already-approved product decisions.

The prompt should preserve existing technical constraints when they materially affect product feasibility, but it should not turn the Product PRD into architecture design.

## Dependencies

The prompt uses stable dependency IDs such as:

```text
DEP-001
DEP-002
```

Dependencies may include:

- another product;
- another capability;
- another team;
- a vendor;
- a data source;
- platform availability;
- legal approval;
- compliance approval;
- commercial agreements;
- funding;
- staffing;
- organizational decisions.

The prompt should not invent dependency ownership.

Unknown ownership should remain explicit.

## Product Strategy and Phases

The Product PRD may describe major phases such as:

- validation;
- initial capability;
- launch;
- expansion;
- migration;
- scaling;
- geographic rollout;
- segment expansion.

The prompt uses stable IDs when useful:

```text
PHASE-001
PHASE-002
```

A phase may capture:

```text
Purpose
Capabilities
Entry Conditions
Exit Conditions
Dependencies
Status
Source
```

The prompt must not assume that every product requires an MVP.

## Roadmap Direction

The roadmap inside a Product PRD is intentionally high-level.

It may show:

- strategic sequencing;
- capability dependencies;
- major milestones;
- required decision points.

It should not become:

- sprint planning;
- engineering estimation;
- implementation scheduling;
- fabricated release commitments.

When dates are not confirmed, sequencing should be used instead.

For example:

```text
PHASE-001
→ validate core workflow

PHASE-002
→ expand to additional customer segment

PHASE-003
→ introduce enterprise integrations
```

## Stakeholders and Governance

The prompt may use stable stakeholder IDs such as:

```text
STK-001
STK-002
```

A stakeholder entry may include:

```text
Role
Interest
Responsibility
Decision Authority
Consulted For
Status
Source
```

Prefer roles over named people unless actual ownership is explicitly known.

The prompt should not invent decision authority.

## Product Risks

The prompt uses stable risk IDs such as:

```text
RISK-001
RISK-002
```

A product risk may capture:

```text
Description
Category
Probability
Impact
Mitigations
Contingency Plan
Related Objective or Capability
Status
Source
```

Possible categories may include:

```text
market
adoption
operational
technical
regulatory
commercial
organizational
dependency
```

These are examples, not mandatory categories.

AI-proposed mitigations must remain hypotheses until confirmed.

## Open Questions, Pending Decisions, and Hypotheses

The workflow explicitly distinguishes:

```text
Open Questions
Pending Decisions
Hypotheses
```

An open question is information that is still unknown.

A pending decision is a known product or strategic choice that has not yet been resolved.

A hypothesis is an assumption that still requires validation.

Examples:

```text
Open Question
→ What is the current activation baseline?
```

```text
Pending Decision
→ Whether the first release targets SMB only or SMB + Mid-Market.
```

```text
Hypothesis
→ Customer support teams may be a secondary user group.
```

## Product and Technical Boundaries

The prompt deliberately separates product-level intent from downstream artifacts.

Conceptually:

```text
Product PRD
→ product-level why, outcomes, capabilities, scope, KPIs

Feature PRD
→ feature-level requirements and acceptance criteria

High-Level Design
→ system-level technical architecture

Feature Design Doc
→ detailed feature-level technical behavior

Implementation plan / LLD
→ implementation detail
```

This prevents the Product PRD from absorbing every later design decision.

## Handling Company and Product Strategy

When company or product strategy is provided, the prompt should:

- use it to understand strategic direction;
- extract only the parts that materially affect the product;
- preserve strategic constraints;
- distinguish strategy from implementation;
- preserve traceability to the source.

The prompt must not invent strategic alignment when no strategy context exists.

## Handling Customer and Market Research

When customer or market research is provided, the prompt should:

- treat research findings as evidence;
- preserve useful references;
- distinguish findings from interpretation;
- distinguish findings from approved product decisions;
- avoid over-generalizing limited research;
- avoid turning a research hypothesis into a confirmed requirement.

Conceptually:

```text
research finding
≠
approved product decision
```

Research informs product decisions.

Research does not automatically define them.

## Handling Analytics and Metrics

When analytics are provided, the prompt should:

- preserve metric definitions when known;
- treat observed values as baselines rather than targets;
- distinguish baseline from target;
- identify measurement gaps;
- avoid assuming analytics instrumentation exists;
- avoid deriving a target automatically from a baseline.

Existing data supports product reasoning.

It does not automatically define success.

## Handling Existing PRDs and Feature PRDs

Existing Product PRDs may contain authoritative decisions that should be preserved.

The prompt should:

- reuse confirmed information;
- identify superseded content;
- detect contradictions;
- avoid duplicating material unnecessarily.

Existing Feature PRDs may provide evidence about already-defined capabilities or behaviors.

A Feature PRD should not silently redefine the broader product strategy.

## Handling Technical Context

Architecture documentation, codebase context, and technical constraints may affect product feasibility.

The prompt should:

- preserve already-approved constraints;
- identify feasibility limitations;
- distinguish current implementation from desired product intent;
- avoid turning the Product PRD into technical design.

Technical context constrains the product.

It does not replace product definition.

## Source Traceability

The prompt preserves the source of important product information when useful.

Sources may include:

- company strategy;
- product strategy;
- customer research;
- market research;
- analytics;
- stakeholder notes;
- business cases;
- roadmap documents;
- existing PRDs;
- project documentation;
- user confirmation.

When detailed grounding would make the Product PRD hard to read, references can be consolidated in the final `References` section.

## Consistency Checks

Before generating the final Product PRD, the prompt performs a consistency review.

It checks questions such as:

- Does the product vision explain why the initiative exists?
- Does the problem align with the vision?
- Is evidence distinguished from assumptions?
- Were audiences or personas invented?
- Are objectives outcome-oriented?
- Does each important objective have a measurable signal or an explicit measurement gap?
- Were KPI targets invented?
- Are metrics and KPIs being treated appropriately?
- Does scope contradict itself?
- Did future considerations accidentally become committed scope?
- Do capabilities support confirmed objectives?
- Are capabilities still high-level?
- Are strategic constraints supported?
- Were technical implementation decisions invented?
- Are dependencies explicit?
- Were dependency owners invented?
- Were roadmap dates invented?
- Do phases align with scope and dependencies?
- Is governance clear?
- Are product risks meaningful?
- Are AI-proposed mitigations still hypotheses?
- Are open questions visible?
- Are pending decisions visible?
- Have authoritative sources been preserved?
- Has the document accidentally become a Feature PRD, HLD, FDD, or implementation plan?

When a material problem prevents a reliable Product PRD, the prompt should return to the relevant stage rather than produce a misleading final document.

## Expected Output

The primary output is a Product Requirements Document in Markdown.

Depending on the available information, the document may contain:

```text
Document Information
Product Vision and Purpose
Strategic Alignment
Context, Problem, and Opportunity
Evidence
Target Audiences
Product Objectives and Outcomes
Success Metrics and KPIs
Scope and Product Boundaries
High-Level Product Capabilities
Strategic Constraints and Existing Decisions
Dependencies
Product Strategy and Phases
Roadmap Direction
Stakeholders and Governance
Product Risks and Mitigations
Open Questions
Pending Decisions
Hypotheses
Candidate Follow-Up Artifacts
References
```

Sections that do not add value should be omitted.

The prompt should not create empty sections simply because the template supports them.

## Optional JSON Output

After generating the Markdown Product PRD, the prompt can optionally generate a structured JSON representation.

The JSON is intended for:

- programmatic consumption;
- automation;
- agent workflows;
- product analysis;
- requirement filtering;
- downstream Feature PRD generation;
- downstream HLD generation;
- structured context exchange.

The Markdown and JSON outputs must represent the same product state.

They should not become two independent interpretations of the product.

Conceptually:

```text
product-definition state
        ├── Markdown → human-readable representation
        └── JSON     → structured representation
```

If both artifacts are stored in a project, teams should avoid maintaining them independently as separate sources of truth.

## Example Usage

A user may start with minimal context:

```text
I want to define a Product PRD for a new internal AI platform for engineering teams.
```

The prompt should inspect available context and begin the product-definition interview.

A richer invocation might be:

```text
Create a Product PRD using the attached company strategy, customer research, analytics, and stakeholder notes.

Do not invent personas, KPI targets, roadmap dates, or product requirements.

Ask me only for product-level information that is materially missing.
```

Another example:

```text
Review the existing product brief, roadmap, research, and Feature PRDs.

Help me consolidate them into a product-level PRD.

Identify contradictions between product strategy, research, and existing requirements before generating the final document.
```

The exact invocation depends on the AI tool and available context.

## Known Limitations

The quality of the Product PRD depends on the information available to the model.

The prompt cannot independently verify:

- company strategy;
- stakeholder agreement;
- customer demand;
- market size;
- research quality;
- hidden business constraints;
- pricing assumptions;
- legal obligations;
- regulatory requirements;
- funding;
- staffing;
- actual roadmap commitments;
- analytics correctness;
- KPI instrumentation;
- technical feasibility beyond the provided context;
- whether an existing PRD is still authoritative.

A polished Product PRD is not proof that the product strategy is correct.

AI-assisted product definition should not replace appropriate validation with:

- product leadership;
- business stakeholders;
- customers or users;
- domain experts;
- engineering;
- design;
- marketing;
- sales;
- support;
- legal;
- compliance;
- finance;
- operations;
- security.

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

- a request that is actually feature-level rather than product-level;
- a product with complete strategic context;
- a product with no documented strategy;
- missing customer evidence;
- conflicting customer research and stakeholder assumptions;
- missing KPI baselines;
- missing KPI targets;
- an AI-suggested target that must remain a hypothesis;
- a Product PRD with future ideas that must remain outside committed scope;
- a capability that becomes too detailed and should move to a Feature PRD;
- roadmap sequencing with no confirmed dates;
- ambiguous stakeholder ownership;
- conflicting existing PRDs;
- technical constraints that materially affect product feasibility;
- a request to generate a partial Product PRD before all stages are complete.

Useful evaluation criteria may include:

- instruction adherence;
- context-first behavior;
- one-primary-question-per-turn compliance;
- per-stage confirmation compliance;
- product-invention rate;
- hypothesis-labeling accuracy;
- source-tracking accuracy;
- audience/persona invention rate;
- evidence-vs-assumption separation;
- objective quality;
- KPI classification accuracy;
- numeric-target invention rate;
- scope consistency;
- capability abstraction quality;
- dependency clarity;
- roadmap-date invention rate;
- stakeholder/governance clarity;
- product-risk quality;
- Product PRD vs. Feature PRD boundary compliance;
- Product PRD vs. technical-design boundary compliance;
- Markdown format compliance;
- JSON validity;
- semantic consistency between Markdown and JSON;
- interview efficiency;
- unnecessary-question rate;
- overall Product PRD usefulness.

Pairwise evaluation may also be useful when comparing future versions of this prompt.

## Maintenance

When changing `prompt.md`, consider updating this document if the change affects:

- interview workflow;
- confirmation behavior;
- product scope;
- inputs;
- status or source rules;
- stable IDs;
- audience handling;
- objective structure;
- KPI / metric classification;
- scope boundaries;
- capability structure;
- roadmap behavior;
- stakeholder / governance handling;
- Product PRD / Feature PRD boundaries;
- technical-design boundaries;
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

- Added a context-first Product PRD workflow.
- Added reuse of strategy documents, product documents, research, analytics, roadmaps, existing PRDs, and stakeholder context.
- Added one-primary-question-per-turn behavior.
- Added mandatory confirmation after every product-definition interview stage.
- Added explicit handling of confirmed information, hypotheses, and unknowns.
- Added source tracking for product information.
- Added stable IDs for audiences, objectives, KPIs, capabilities, decisions, dependencies, phases, stakeholders, risks, and hypotheses.
- Added safeguards against silent product strategy or requirement invention.
- Added explicit distinction between Product PRD and Feature PRD.
- Added explicit separation between product definition and technical design.
- Added product vision, problem, opportunity, and evidence modeling.
- Added audience and optional persona modeling without fictional-persona defaults.
- Added outcome-oriented product objectives.
- Added metric, KPI, and guardrail-metric classification.
- Added scope, future-consideration, and product-boundary handling.
- Added high-level product capability modeling.
- Added strategic constraint and existing-decision handling.
- Added dependency tracking.
- Added product strategy, phase, and roadmap-direction handling without invented dates.
- Added stakeholder and governance modeling.
- Added product risk and mitigation tracking.
- Added open-question, pending-decision, and hypothesis handling.
- Added consistency checks before final document generation.
- Added source traceability and references.
- Added Markdown output with optional structured JSON representation.

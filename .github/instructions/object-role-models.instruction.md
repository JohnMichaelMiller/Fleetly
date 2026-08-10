---
ai_generated: true
model: "openai/gpt-5.3-codex@2026-08"
operator: "johnmillerATcodemag-com"
chat_id: "create-object-role-models-instruction-20260806"
prompt: |
  using the content at https://orm.net/, create an instruction file for Object Role Models
started: "2026-08-06T00:40:00Z"
ended: "2026-08-06T01:05:00Z"
task_durations:
  - task: "source review from orm.net"
    duration: "00:12:00"
  - task: "instruction authoring"
    duration: "00:11:00"
  - task: "validation and formatting"
    duration: "00:02:00"
total_duration: "00:25:00"
ai_log: "ai-logs/2026/08/06/create-object-role-models-instruction-20260806/conversation.md"
source: "https://orm.net/"
---

# Object Role Modeling Instruction Guide

## Introduction

Use this instruction when modeling a business domain with Object Role Modeling (ORM). ORM is a fact-oriented approach for conceptual modeling and querying where the domain is captured in terms of objects playing roles in fact types, using language that can be validated by domain experts.

## Audience and Scope

- Audience: Data modelers, solution architects, analysts, and engineers producing conceptual data models.
- Scope: Conceptual schema modeling with ORM 2, including fact types, constraints, verbalization, validation, and conceptual querying.
- Out of scope: Physical database tuning, vendor-specific indexing, and UI design.

## Prerequisites

- A clear business domain and glossary of business terms.
- Access to subject matter experts for model validation.
- Basic familiarity with conceptual modeling.
- Optional tool support for ORM 2, such as NORMA.

## Output Requirements

- Produce a conceptual ORM model that is fact-oriented and attribute-free.
- Express knowledge as elementary facts, constraints, and derivation rules when relevant.
- Include textual verbalizations suitable for non-technical review.
- Record key assumptions, unresolved issues, and validation outcomes.

## Steps / Procedure

1. Define the universe of discourse.
   - Identify the business boundary and core vocabulary.
   - Document object types and their intended meaning.
2. Capture elementary fact types.
   - Model facts as relationships where objects play roles.
   - Prefer elementary (atomic) fact expressions that are easy to verbalize.
3. Add identification and reference schemes.
   - Specify how each object type is identified.
   - Validate naming and reference consistency with domain language.
4. Apply core constraints.
   - Add uniqueness constraints (including spanning uniqueness where needed).
   - Add mandatory role constraints.
   - Add value, subtype, subset/equality, exclusion, frequency, ring, and join constraints as needed.
5. Model advanced structures carefully.
   - Use objectification only when justified by business semantics.
   - For objectification, verify identification and uniqueness implications.
6. Validate through verbalization.
   - Generate natural-language readings for facts and constraints.
   - Review verbalizations with domain experts and refine terminology.
7. Test with conceptual queries.
   - Formulate path-based conceptual queries over the model.
   - Confirm the model supports required business questions without exposing physical storage details.
8. Prepare for logical mapping.
   - Apply approved transformations for relational mapping.
   - Preserve conceptual clarity while optimizing where required.

## Examples / Samples

```example
Domain: Course Enrollment

Elementary facts:
- Student enrolls in Course.
- Course is offered by Department.
- Student has StudentNumber.

Constraints:
- Each Student has exactly one StudentNumber (uniqueness + mandatory).
- A Student may enroll in many Courses.
- Each Course is offered by exactly one Department.

Verbalization:
- Each student has exactly one student number.
- Each course is offered by exactly one department.
```

## Templates / Snippets

```markdown
# <Domain Name> ORM Conceptual Model

## Universe of Discourse

- Business boundary: <scope>
- Domain glossary: <terms>

## Object Types

- <ObjectType>: <definition>

## Elementary Fact Types

- <Reading 1>
- <Reading 2>

## Identification and Reference Schemes

- <ObjectType> is identified by <reference scheme>

## Constraints

- Uniqueness: <details>
- Mandatory roles: <details>
- Other constraints: <value/subtype/subset/equality/exclusion/frequency/ring/join>

## Objectification (if used)

- Fact type objectified: <fact type>
- Rationale: <why needed>
- Constraint implications: <notes>

## Verbalization Review

- Reviewer: <name>
- Outcomes: <accepted changes>

## Conceptual Queries

- Query 1: <business question>
- Query 2: <business question>

## Assumptions and Open Issues

- Assumption: <statement>
- Open issue: <question>
```

## Validation / Quality Checklist

- [ ] Model is fact-oriented and attribute-free at conceptual level.
- [ ] Facts are elementary and clearly verbalizable.
- [ ] Object identification/reference schemes are explicit.
- [ ] Required constraints are modeled and unambiguous.
- [ ] Objectification usage is justified and reviewed.
- [ ] Domain experts validated key verbalizations.
- [ ] Conceptual queries align with business questions.
- [ ] Mapping considerations do not degrade conceptual clarity.

## File Placement and Naming

- Folder: .github/instructions/
- Filename: object-role-models.instruction.md

## Versioning and Ownership

- Owner: Data modeling maintainers
- Last updated: 2026-08-06
- Change policy: Update via pull request with rationale, impacted sections, and checklist confirmation.

## Security and Privacy

- Do not include secrets, credentials, or private keys.
- Redact personal or regulated data in examples.
- Use synthetic sample data for demonstrations.

## References / Glossary

- Source site: https://orm.net/
- ORM Overview: https://orm.net/overview.html
- Modeling Issues: https://orm.net/issues.html
- Conceptual Queries: https://orm.net/queries.html
- UML and ORM: https://orm.net/uml_orm.html
- ORM: Object Role Modeling, a fact-oriented conceptual modeling approach.
- Elementary fact: An atomic fact expression modeled at conceptual level.
- Verbalization: Natural-language rendering of model facts and constraints for validation.
- Objectification: Treating a fact instance as an object type when semantically justified.

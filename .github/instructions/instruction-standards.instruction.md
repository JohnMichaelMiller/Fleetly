---
ai_generated: true
model: "openai/gpt-5.3-codex@2026-08"
operator: "johnmillerATcodemag-com"
chat_id: "execute-prompt-create-instruction-files-20260806"
prompt: |
  Generate a Markdown authoring guide for creating instruction files with recommended sections,
  placement, naming, and a validation checklist.
started: "2026-08-06T00:00:00Z"
ended: "2026-08-06T00:10:00Z"
task_durations:
  - task: "requirements extraction"
    duration: "00:03:00"
  - task: "document authoring"
    duration: "00:06:00"
  - task: "final validation"
    duration: "00:01:00"
total_duration: "00:10:00"
ai_log: "ai-logs/2026/08/06/execute-prompt-create-instruction-files-20260806/conversation.md"
source: ".github/prompts/create-instruction-file-instructions.prompt.md"
---

# Instruction File Authoring Guide

## Introduction

Use this guide when creating or updating repository instruction files so contributors can follow a consistent, reviewable, and maintainable format. Apply it whenever you are documenting procedures, standards, guardrails, or authoring workflows that should live as reusable project instructions.

## Audience and Scope

- Audience: Contributors authoring instruction files for this repository.
- Scope: Standard sections, directory placement, naming conventions, reusable template usage, examples, and quality validation.
- Out of scope: General coding standards, runtime behavior documentation, and product/user documentation that does not define instruction authoring patterns.

## File Placement and Naming Conventions

- Folder: `.github/instructions/`
- Filenames: hyphenated lowercase and must end with `.instruction.md`
- One instruction file per topic
- Keep names specific to the subject, for example: `linting-workflow.instruction.md`

## Standard Sections (overview)

Each instruction file should include these sections:

- Introduction: What this instruction covers and when to use it.
- Audience and Scope: Who should use it; what is included and excluded.
- Prerequisites: Tools, permissions, or context needed before starting.
- Output Requirements: Exact outputs, formats, paths, and constraints.
- Steps / Procedure: Ordered, actionable instructions.
- Examples / Samples: Minimal but complete examples.
- Templates / Snippets: Reusable copy-paste blocks.
- Validation / Quality Checklist: Verifiable completeness and quality checks.
- File Placement and Naming: Correct location and filename convention.
- Versioning and Ownership: Maintainer and update expectations.
- Security and Privacy: Handling of sensitive data and redaction guidance.
- References / Glossary: Optional links and definitions.

## Copy/Paste Template (complete skeleton)

````markdown
# Instruction File Title

## Introduction

<Brief purpose, when to use, and outcomes.>

## Audience and Scope

- Audience: <Who>
- Scope: <What's included>
- Out of scope: <What's not covered>

## Prerequisites

- <Tool/permission/context>

## Output Requirements

- <Exact output path(s)/formats>
- <No extra commentary/wrappers>

## Steps / Procedure

1. <Step>
2. <Step>
3. <Step>

## Examples / Samples

```example
<Short, complete example>
```

## Templates / Snippets

```markdown
<Reusable snippet or section>
```

## Validation / Quality Checklist

- [ ] Outputs and formats match requirements
- [ ] Steps are actionable and ordered
- [ ] Examples run or render as expected
- [ ] No secrets or sensitive data
- [ ] Naming and placement adhere to conventions

## File Placement and Naming

- Folder: `.github/instructions/`
- Filename: `<topic-name>.instruction.md`

## Versioning and Ownership

- Owner: <name/role>
- Last updated: YYYY-MM-DD
- Change policy: <how to propose changes>

## Security and Privacy

- <Redaction, secrets handling, PII guidance>

## References / Glossary

- <Links and definitions>
````

## Section-by-Section Guidance

- Title: Be specific and topic-focused, such as "CI Pipeline Instructions".
- Prerequisites: Include only what is required; link setup docs where possible.
- Output Requirements: State exact path, format, and overwrite behavior.
- Steps / Procedure: Use numbered steps with one action per step and expected result.
- Examples / Samples: Keep examples short, realistic, and runnable/renderable.
- Templates / Snippets: Provide reusable blocks with clear placeholders.
- Validation / Quality Checklist: Use concise, verifiable checks.
- Versioning and Ownership: Assign a clear owner and keep date fields current.
- Security and Privacy: Exclude secrets; use redacted examples when needed.

## Example (concise but realistic)

Title: Linting Instructions

- Audience: Contributors
- Scope: How to run and interpret linting locally

- Output Requirements:
  - Provide a passing lint run example output excerpt

- Steps / Procedure:
  1. Install dependencies
  2. Run linter
  3. Fix reported issues and re-run

- Example:

```text
$ tool lint
✔ No issues found
```

## Quality Checklist

- [ ] Title and purpose are clear
- [ ] Steps are ordered and testable
- [ ] Examples run or render
- [ ] Output path and format are explicit
- [ ] File lives under `.github/instructions/` and ends with `.instruction.md`
- [ ] Security and privacy guidance is included
- [ ] Owner and last-updated fields are present

## Versioning and Ownership

- Owner: Repository maintainers for instructions under `.github/instructions/`
- Last updated: 2026-08-06
- Change policy: Propose updates via pull request; include rationale, affected files, and checklist confirmation.

## Security and Privacy

- Do not include secrets, tokens, credentials, private keys, or personal data.
- Redact sensitive values in samples, logs, and screenshots.
- Use placeholders for confidential endpoints, IDs, and account names.
- Reference repository security policy when handling uncertain data classifications.

## References / Glossary

- Instruction file: A repository-scoped markdown file that defines a repeatable process or governance rule.
- Topic-based instruction: A single-purpose instruction file covering one process area.
- Kebab case: Lowercase words separated by hyphens, for example `release-checklist`.
- Related guidance: `.github/instructions/ai-assisted-output.instructions.md`

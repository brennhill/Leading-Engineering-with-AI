---
feature: <feature-name>
status: draft # draft | active | deprecated
spec: /solution-design/<spec-file>.md
code_paths:
  - /path/to/primary/file
  - /path/to/secondary/file
tests:
  - /path/to/test-file
owner: @team-or-person
last_updated: YYYY-MM-DD
related_docs:
  - /docs/<related-doc>.md
runbook: /AI-operations.md
risk_tier: low # low | medium | high
feature_flag: <flag-name-or-none>
---

# <Feature Name>

## Problem
What user or business problem does this feature solve?

## Scope
What is in scope and explicitly out of scope?

## Behavior contract
Describe expected behavior in plain language.
Include edge cases and failure behavior.

## Control boundaries
What the LLM/agent can do:

What the LLM/agent cannot do:

Human approval/override points:

## Code map
Briefly explain how key files work together.

## Test map
List critical tests and what each test protects.

## Known risks
List top risks, likely failure modes, and mitigations.

## Change checklist
- [ ] Header links are accurate.
- [ ] Tests were updated.
- [ ] Backward compatibility reviewed.
- [ ] Docs and examples updated.
